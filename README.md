# keyword-mining
API to extract keywords from a text.

The algorithm extracts all nominal groups (candidate keywords) from the text and, for each one, attributes a score based on multiple parameters including the number of occurrences.
The final list of keywords is composed of best-scored nominal groups.

### Note
For the moment, this tool works only for English and French.

## INSTALL AND RUN

### REQUIREMENTS
This tool requires *Python2.7* (not working for *Python3*).

### WITH PIP
```
git clone https://github.com/AnthonySigogne/keyword-mining.git
cd keyword-mining
pip install -r requirements.txt
```

Then, run the tool :
```
FLASK_APP=index.py flask run
```

To run in debug mode, prepend `FLASK_DEBUG=1` to the command :
```
FLASK_DEBUG=1 ... flask run
```

### WITH DOCKER
To run the tool with Docker, you can use my DockerHub image :
https://hub.docker.com/r/anthonysigogne/keyword-mining/
```
docker run -p 5000:5000 anthonysigogne/keyword-mining
```

Or, build yourself a Docker image :
```
git clone https://github.com/AnthonySigogne/keyword-mining.git
cd keyword-mining
docker build -t keyword-mining .
```

## USAGE AND EXAMPLES
To list all services of API, type this endpoint in your web browser : http://localhost:5000/

### FROM A TEXT
Index a web page through its URL.

* **URL**

  /keywords_from_text

* **Method**

  `POST`

* **Form Data Params**

  **Required:**

  `text=[string]`, the text to analyze  

  **Not required:**

  `hits=[int]`, limit number of keywords returned, 100 by default

* **Success Response**

  * **Code:** 200 <br />
    **Content:**
    ```
    {
      "keywords": [
        "computer science PhD in applied Language",
        "PhD in Computer Science",
        "Creation of ergonomic websites",
        "Modern infrastructure with API",
        "Development of effective application",
        "experience of research laboratories",
        "projects for international clients",
        "Computer courses for individuals",
        ...
      ]
    }
    ```

* **Error Response**

  * **Code:** 400 INVALID USAGE <br />


* **Sample Call (with cURL)**

  ```
  curl http://localhost:5000/keywords_from_text --data "text=True programming enthusiast, I quickly oriented to computer studies at the university, until a computer science PhD in applied Language Processing."
  ```

### FROM AN URL
Query engine to find a list of relevant URLs.
Return the sublist of matching URLs sorted by relevance, and the total of matching URLs, in JSON.

* **URL**

  /search

* **Method**

  `POST`

* **Form Data Params**

  **Required:**

  `url=[string]`, the url to analyze  

  **Not required:**

  `hits=[int]`, limit number of keywords returned, 100 by default

* **Success Response**

  * **Code:** 200 <br />
    **Content:**
    ```
    {
      "keywords": [
        "computer science PhD in applied Language",
        "PhD in Computer Science",
        "Creation of ergonomic websites",
        "Modern infrastructure with API",
        "Development of effective application",
        "experience of research laboratories",
        "projects for international clients",
        "Computer courses for individuals",
        ...
      ]
    }
    ```

* **Error Response**

  * **Code:** 400 INVALID USAGE <br />


* **Sample Call (with cURL)**

  ```
  curl http://localhost:5000/keywords_from_url --data "url=https://www.byprog.com/en"
  ```  


## FUTURE FEATURES
* index more page features like keywords,...
* better scoring function
* filter bad results

## LICENCE
MIT
