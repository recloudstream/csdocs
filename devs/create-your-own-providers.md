import kotlinx.coroutines.runBlocking
import org.jsoup.Jsoup
import org.jsoup.nodes.Element

class FaselHDProvider : Provider {
    override suspend fun search(query: String): List<SearchResponse> {
        val document = Jsoup.connect("https://w1.faselhdtv.top/search")
            .data("query", query)
            .get()

        return document.select("div.movie").mapNotNull {
            it.toSearchResponse()
        }
    }

    private fun Element.toSearchResponse(): SearchResponse? {
        val link = this.select("a").first() ?: return null
        val href = link.attr("href")
        val img = this.select("img").first()
        val title = img?.attr("alt") ?: return null
        val posterUrl = img.attr("src")

        return SearchResponse(
            title = title,
            url = href,
            posterUrl = posterUrl
        )
    }

    override val mainPage = mainPageOf(
        Pair("1", "Latest Movies"),
        Pair("2", "Popular Movies")
    )

    override suspend fun getMainPage(
        page: Int,
        request: MainPageRequest
    ): HomePageResponse {
        val url = when (request.data) {
            "1" -> "https://w1.faselhdtv.top/latest-movies?page=$page"
            "2" -> "https://w1.faselhdtv.top/popular-movies?page=$page"
            else -> throw IllegalArgumentException("Unknown request data: ${request.data}")
        }

        val document = Jsoup.connect(url).get()
        val movies = document.select("div.movie").mapNotNull {
            it.toSearchResponse()
        }

        return HomePageResponse(
            request.name,
            movies
        )
    }

    override suspend fun load(url: String): LoadResponse {
        val document = Jsoup.connect(url).get()
        val details = document.select("div.details")

        val title = details.select("h1.title").text()
        val posterUrl = details.select("img.poster").attr("src")
        val plot = details.select("div.plot").text()
        val year = details.select("span.year").text().toIntOrNull()
        val tags = details.select("span.tags a").map { it.text() }
        val cast = details.select("span.cast a").map { it.text() }
        val rating = details.select("span.rating").text().toFloatOrNull()
        val trailer = details.select("a.trailer").attr("href")

        val episodes = document.select("div.episode").mapIndexed { index, element ->
            val episodeTitle = element.select("a").text()
            val episodeUrl = element.select("a").attr("href")
            Episode(
                title = episodeTitle,
                url = episodeUrl,
                season = 1,
                episode = index + 1
            )
        }

        return if (url.contains("/movie/")) {
            MovieLoadResponse(
                title = title,
                url = url,
                posterUrl = posterUrl,
                plot = plot,
                year = year,
                tags = tags,
                cast = cast,
                rating = rating,
                trailer = trailer
            )
        } else {
            TvSeriesLoadResponse(
                title = title,
                url = url,
                posterUrl = posterUrl,
                plot = plot,
                year = year,
                tags = tags,
                cast = cast,
                rating = rating,
                episodes = episodes
            )
        }
    }

    override suspend fun loadLinks(url: String): List<VideoLink> {
        val document = Jsoup.connect(url).get()
        return document.select("div.video-player a").mapNotNull { element ->
            val videoUrl = element.attr("href")
            if (videoUrl.isNotEmpty()) {
                VideoLink(
                    url = videoUrl,
                    quality = "Unknown"
                )
            } else {
                null
            }
        }
    }
}
