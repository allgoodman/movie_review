import requests
from bs4 import BeautifulSoup

def get_reviews(movie_name):
    # IMDb URL for the search results page
    search_url = "https://www.imdb.com/find?q=" + movie_name + "&s=tt&ref_=fn_al_tt_mr"

    # Make a request to the search URL
    response = requests.get(search_url)
    soup = BeautifulSoup(response.content, "html.parser")

    # Find the first search result (movie)
    first_result = soup.find("td", class_="result_text")
    movie_url = first_result.a["href"]

    # Make a request to the movie URL
    response = requests.get("https://www.imdb.com" + movie_url)
    soup = BeautifulSoup(response.content, "html.parser")

    # Find the section containing the reviews
    reviews_section = soup.find("div", class_="lister-list")
    review_elements = reviews_section.find_all("div", class_="text show-more__control")

    # Extract the text from each review
    reviews = [review.text.strip() for review in review_elements]

    return reviews

# Example usage
reviews = get_reviews("The Shawshank Redemption")
for review in reviews:
    print(review)
