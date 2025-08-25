# Coursera Scraping Project
Coursera is an e-learning platform hosting thousands of courses from various institutions and instructors.  
The goal of this project is to collect structured information from Coursera's Courses and store them in a PostgreSQL database.  
These Data should be accessible through a simple API.


## Expectations
- The candidate may choose **Python or Go** along with any preferred framework.
- The data should be stored in a **PostgreSQL** database.
- The project should include a simple API to access the data.
- The project must include a Readme file with instructions on how to run the scraper and query the API. 
- The content can be scraped using simple HTTP requests, some details are provided in the "How to Start" section, however the scraping strategy is up to the candidate.
- The implementation must allow **multiple scrapes of the entire site without inserting duplicate records** into the database.
- It is essential to do not overload Coursera's servers with too many requests in a short period of time.
- [Optional] Use Docker to containerize the application.


## Required Data
Coursera offers courses, degrees, certificates, and more.  
For this project, only the courses listed in the following sitemap are relevant:  

👉 [Courses Sitemap](https://www.coursera.org/sitemap~www~courses.xml)

For each course, the scraper should collect and store:

- **Course URL**  
- **Course name**  
- **Instructors' names**  
- **Skills** (as listed on the course page)

If any of these fields are missing for a given course, the course may be skipped.


## APIs Requirements
The APIs should allow:
- Retrieving a single course by **Course URL**
```json
{
    "url": "https://www.coursera.org/learn/ethical-ai-use",
    "name": "Ethical AI Use",
    "instructors": ["Instructor 1", "Instructor 2"],
    "skills": ["AI Ethics", "Responsible AI"]
}
```

- Search for one or multiple courses by Name, Instructor(s), and/or Skill(s)
```json
[
    {
        "url": "https://www.coursera.org/learn/ethical-ai-use",
        "name": "Ethical AI Use",
        "instructors": ["Instructor 1", "Instructor 2"],
        "skills": ["AI Ethics", "Responsible AI"]
    },
    {
        "url": "https://www.coursera.org/learn/machine-learning",
        "name": "Machine Learning",
        "instructors": ["Instructor 3"],
        "skills": ["Machine Learning", "Data Science"]
    }
]
```

# How to Start
Use the sitemap to extract a list of course URLs.

Example course URL:
https://www.coursera.org/learn/ethical-ai-use

## Course name:
Found inside the h1 element with attribute data-e2e="hero-title".

```html
<h1 class="cds-119 css-1rmg2ag cds-121" data-e2e="hero-title">Ethical AI Use</h1>
```

## Skills:
Located within the div that contains:
```html
<h2 class="css-fk6qfz">Skills you'll gain</h2>
```

The skills themselves are listed as <li> elements inside this section.

## Instructors (only visible ones):
Found in the div containing:

```html
<h3 class="cds-119 cds-Typography-base css-h1jogs cds-121"><span>Instructor</span></h3>
```

## Optional:
If multiple instructors are present, the complete list can be retrieved from the container with:

```html
data-testid="scroll-container"
```
This section stores the full instructor list, even if only a subset is initially visible.
