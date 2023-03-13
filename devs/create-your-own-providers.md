---
label: Creating your own providers
order: 998
icon: repo
---

# Creating your own Providers

Providers in CloudStream consists primarily of 4 different parts:

- [Searching](https://recloudstream.github.io/dokka/app/com.lagradost.cloudstream3/-main-a-p-i/index.html#498495168%2FFunctions%2F492899073)
- [Loading the home page](https://recloudstream.github.io/dokka/app/com.lagradost.cloudstream3/-main-a-p-i/index.html#1356482668%2FFunctions%2F492899073)
- [Loading the show page](https://recloudstream.github.io/dokka/app/com.lagradost.cloudstream3/-main-a-p-i/index.html#1671784382%2FFunctions%2F492899073)
- [Loading the video links](https://recloudstream.github.io/dokka/app/com.lagradost.cloudstream3/-main-a-p-i/index.html#-930139416%2FFunctions%2F492899073)

When making a provider it is important that you are confident you can scrape the video links first!
Video links are often the most protected part of the website and if you cannot scrape them then the provider is useless.

## 0. Scraping

If you are unfamiliar with the concept of scraping, you should probably start by reading [this guide](scraping/gettingstarted/) which should hopefuly familiarize you with this technique.

## 1. Searching

This one is probably the easiest, based on a query you should return a list of [SearchResponse](https://recloudstream.github.io/dokka/app/com.lagradost.cloudstream3/-search-response/index.html)

Scraping the search results is essentially just finding the search item elements on the site (red box) and looking in them to find name, url and poster url and put the data in a SearchResponse.

![image](https://user-images.githubusercontent.com/46196380/184509999-0a50d13d-bc89-4f61-9f6e-f36648de0510.png)

The code for the search then ideally looks something like

```kotlin
// (code for Eja.tv)

override suspend fun search(query: String): List<SearchResponse> {
    return app.post(
        mainUrl, data = mapOf("search" to query) // Fetch the search data
    ).document // Convert the response to a searchable document  
        .select("div.card-body") // Only select the search items using a CSS selector
        .mapNotNull { // Convert all html elements to SearchResponses and filter out the null search results
            it.toSearchResponse()
        }
}

// Converts a html element to a useable search response
// Basically just look in the element for sub-elements with the data you want
private fun Element.toSearchResponse(): LiveSearchResponse? {
    // If no link element then it's no a valid search response
    val link = this.select("div.alternative a").last() ?: return null
    // fixUrl is a built in function to convert urls like /watch?v=..... to https://www.youtube.com/watch?v=.....
    val href = fixUrl(link.attr("href"))
    val img = this.selectFirst("div.thumb img")
    // Optional parameter, scraping languages are not required but might be nice on some sites
    val lang = this.selectFirst(".card-title > a")?.attr("href")?.removePrefix("?country=")
        ?.replace("int", "eu") //international -> European Union 🇪🇺
        
    // There are many types of searchresponses but mostly you will be using AnimeSearchResponse, MovieSearchResponse
    // and TvSeriesSearchResponse, all with different parameters (like episode count)
    return LiveSearchResponse(
        // Kinda hack way to get the title
        img?.attr("alt")?.replaceFirst("Watch ", "") ?: return null,
        href,
        this@EjaTv.name,
        TvType.Live,
        fixUrl(img.attr("src")),
        lang = lang
    )
}
```

In this code snippet I have separated the Element to SearchResult conversion to a separate function because that function can often be used when scraping the home page later. No need to parse the same type of element twice.

## 2. Loading the home page

Getting the homepage is essentially the same as getting search results but with a twist: you define the queries in a variable like this:

```kotlin

override val mainPage = mainPageOf(
        Pair("1", "Recent Release - Sub"),
        Pair("2", "Recent Release - Dub"),
        Pair("3", "Recent Release - Chinese"),
    )
```

This dictates what the getMainPage function will be receiving as function arguments.
Basically when the recent dubbed shows should be loaded the getMainPage gets called with a page number and the request you defined above.

```kotlin

override suspend fun getMainPage(
        page: Int,
        request : MainPageRequest
    ): HomePageResponse {

    // page: An integer > 0, starts on 1 and counts up, Depends on how much the user has scrolled.
    // request.data == "2"
    // request.name == "Recent Release - Dub"

```

With these variables you should fetch the appropriate list of Search Response like this:

```kotlin

// Gogoanime
override suspend fun getMainPage(
        page: Int,
        request : MainPageRequest
    ): HomePageResponse {
        // Use the data you defined earlier in the pair to send the request you want.
        val params = mapOf("page" to page.toString(), "type" to request.data)
        val html = app.get(
            "https://ajax.gogo-load.com/ajax/page-recent-release.html",
            headers = headers,
            params = params
        )
        val isSub = listOf(1, 3).contains(request.data.toInt())

        // In this case a regex is used to get all the correct variables
        // But if you defined the Element.toSearchResponse() earlier you can often times use it on the homepage
        val home = parseRegex.findAll(html.text).map {
            val (link, epNum, title, poster) = it.destructured
            newAnimeSearchResponse(title, link) {
                this.posterUrl = poster
                addDubStatus(!isSub, epNum.toIntOrNull())
            }
        }.toList()

        // Return a list of search responses mapped to the request name defined earlier.
        return newHomePageResponse(request.name, home)
    }
```

This might seem needlessly convoluted, but this system is to allow "infinite" loading, e.g loading the next page of search
responses when the user has scrolled to the end.

TLDR: Exactly like searching but you defined your own queries.


## 3. Loading the show page

// Currently Work in progress 

The home page is a bit more complex than search results, but it uses the same logic used to get search results: using CSS selectors and regex to parse html into kotlin object. With the amount of info being parsed this function can get quite big, but the fundamentals are still pretty simple.

A function can look something like this:


```kotlin

    // The url argument is the same as what you put in the Search Response from search() and getMainPage() 
    override suspend fun load(url: String): LoadResponse {
        val document = app.get(url).document

        val details = document.select("div.detail_page-watch")
        val img = details.select("img.film-poster-img")
        val posterUrl = img.attr("src")
        // It's safe to throw errors here, they will be shown to the user and can help debugging. 
        val title = img.attr("title") ?: throw ErrorLoadingException("No Title")

        var duration = document.selectFirst(".fs-item > .duration")?.text()?.trim()
        var year: Int? = null
        var tags: List<String>? = null
        var cast: List<String>? = null
        val youtubeTrailer = document.selectFirst("iframe#iframe-trailer")?.attr("data-src")
        val rating = document.selectFirst(".fs-item > .imdb")?.text()?.trim()
            ?.removePrefix("IMDB:")?.toRatingInt()

        // I would not really recommend 
        document.select("div.elements > .row > div > .row-line").forEach { element ->
            val type = element?.select(".type")?.text() ?: return@forEach
            when {
                type.contains("Released") -> {
                    year = Regex("\\d+").find(
                        element.ownText() ?: return@forEach
                    )?.groupValues?.firstOrNull()?.toIntOrNull()
                }
                type.contains("Genre") -> {
                    tags = element.select("a").mapNotNull { it.text() }
                }
                type.contains("Cast") -> {
                    cast = element.select("a").mapNotNull { it.text() }
                }
                type.contains("Duration") -> {
                    duration = duration ?: element.ownText().trim()
                }
            }
        }
        val plot = details.select("div.description").text().replace("Overview:", "").trim()

        val isMovie = url.contains("/movie/")

        // https://sflix.to/movie/free-never-say-never-again-hd-18317 -> 18317
        val idRegex = Regex(""".*-(\d+)""")
        val dataId = details.attr("data-id")
        val id = if (dataId.isNullOrEmpty())
            idRegex.find(url)?.groupValues?.get(1)
                ?: throw ErrorLoadingException("Unable to get id from '$url'")
        else dataId

        val recommendations =
            document.select("div.film_list-wrap > div.flw-item").mapNotNull { element ->
                val titleHeader =
                    element.select("div.film-detail > .film-name > a") ?: return@mapNotNull null
                val recUrl = fixUrlNull(titleHeader.attr("href")) ?: return@mapNotNull null
                val recTitle = titleHeader.text() ?: return@mapNotNull null
                val poster = element.select("div.film-poster > img").attr("data-src")
                MovieSearchResponse(
                    recTitle,
                    recUrl,
                    this.name,
                    if (recUrl.contains("/movie/")) TvType.Movie else TvType.TvSeries,
                    poster,
                    year = null
                )
            }

        if (isMovie) {
            // Movies
            val episodesUrl = "$mainUrl/ajax/movie/episodes/$id"
            val episodes = app.get(episodesUrl).text

            // Supported streams, they're identical
            val sourceIds = Jsoup.parse(episodes).select("a").mapNotNull { element ->
                var sourceId = element.attr("data-id")
                if (sourceId.isNullOrEmpty())
                    sourceId = element.attr("data-linkid")

                if (element.select("span").text().trim().isValidServer()) {
                    if (sourceId.isNullOrEmpty()) {
                        fixUrlNull(element.attr("href"))
                    } else {
                        "$url.$sourceId".replace("/movie/", "/watch-movie/")
                    }
                } else {
                    null
                }
            }

            val comingSoon = sourceIds.isEmpty()

            return newMovieLoadResponse(title, url, TvType.Movie, sourceIds) {
                this.year = year
                this.posterUrl = posterUrl
                this.plot = plot
                addDuration(duration)
                addActors(cast)
                this.tags = tags
                this.recommendations = recommendations
                this.comingSoon = comingSoon
                addTrailer(youtubeTrailer)
                this.rating = rating
            }
        } else {
            val seasonsDocument = app.get("$mainUrl/ajax/v2/tv/seasons/$id").document
            val episodes = arrayListOf<Episode>()
            var seasonItems = seasonsDocument.select("div.dropdown-menu.dropdown-menu-model > a")
            if (seasonItems.isNullOrEmpty())
                seasonItems = seasonsDocument.select("div.dropdown-menu > a.dropdown-item")
            seasonItems.apmapIndexed { season, element ->
                val seasonId = element.attr("data-id")
                if (seasonId.isNullOrBlank()) return@apmapIndexed

                var episode = 0
                val seasonEpisodes = app.get("$mainUrl/ajax/v2/season/episodes/$seasonId").document
                var seasonEpisodesItems =
                    seasonEpisodes.select("div.flw-item.film_single-item.episode-item.eps-item")
                if (seasonEpisodesItems.isNullOrEmpty()) {
                    seasonEpisodesItems =
                        seasonEpisodes.select("ul > li > a")
                }
                seasonEpisodesItems.forEach {
                    val episodeImg = it?.select("img")
                    val episodeTitle = episodeImg?.attr("title") ?: it.ownText()
                    val episodePosterUrl = episodeImg?.attr("src")
                    val episodeData = it.attr("data-id") ?: return@forEach

                    episode++

                    val episodeNum =
                        (it.select("div.episode-number").text()
                            ?: episodeTitle).let { str ->
                            Regex("""\d+""").find(str)?.groupValues?.firstOrNull()
                                ?.toIntOrNull()
                        } ?: episode

                    episodes.add(
                        newEpisode(Pair(url, episodeData)) {
                            this.posterUrl = fixUrlNull(episodePosterUrl)
                            this.name = episodeTitle?.removePrefix("Episode $episodeNum: ")
                            this.season = season + 1
                            this.episode = episodeNum
                        }
                    )
                }
            }
```

# TODO: REST
