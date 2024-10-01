# Architecture Overview

The final project for this course consists of several steps that you must complete. The high-level step list below provides an overview of the complete project. The project is divided into smaller labs with detailed instructions for each step. You must complete all labs to successfully complete the project.

## Project Breakdown

1. **Fork the GitHub repo containing the project template.**
   - The main web application is a predefined Django application. You will need to add new features, then build and run your project implementation.
   - Fork the repository in your account.
   - Clone the repository in the Cloud IDE environment.

2. **Create static pages to finish the user stories.**
   - Run the application locally.
   - Add user management to the Django application.
   - Implement user management using the Django user authentication system and create a REACT frontend.

3. **Implement backend services.**
   - Create a Node.js server to manage dealers and reviews using MongoDB and dockerize it.
   - Deploy the sentiment analyzer on Code Engine.
   - Create Django models and views to manage car models and car makes.
   - Create Django proxy services and views to integrate dealers and reviews together.

4. **Add dynamic pages with Django templates.**
   - Create a page that displays all the dealers.
   - Create a page that displays reviews for a selected dealer.
   - Create a page that lets the end user add a review for a selected dealer.

5. **Implement CI/CD, and then run and test your application.**
   - Set up continuous integration and delivery for code linting.
   - Run your application on Cloud IDE.
   - Test the updated application locally.
   - Deploy the application on Kubernetes.

## Solution Architecture

The solution will consist of multiple technologies:

- The user interacts with the **"Dealerships Website,"** a Django website, through a web browser.

### Django Application Microservices

The Django application provides the following microservices for the end user:

- `get_cars/` - To get the list of cars from
- `get_dealers/` - To get the list of dealers
- `get_dealers/:state` - To get dealers by state
- `dealer/:id` - To get dealer by id
- `review/dealer/:id` - To get reviews specific to a dealer
- `add_review/` - To post a review about a dealer

The Django application uses an SQLite database to store the Car Make and Car Model data.

### Dealerships and Reviews Service

The **"Dealerships and Reviews Service"** is an Express Mongo service running in a Docker container. It provides the following services:

- `/fetchDealers` - To fetch the dealers
- `/fetchDealer/:id` - To fetch the dealer by id
- `/fetchReviews` - To fetch all the reviews
- `/fetchReview/dealer/:id` - To fetch reviews for a dealer by id
- `/insertReview` - To insert a review

**"Dealerships Website"** interacts with the **"Dealership and Reviews Service"** through the **"Django Proxy Service"** contained within the Django application.

### Sentiment Analyzer Service

The **"Sentiment Analyzer Service"** is deployed on IBM Cloud Code Engine, providing the following service:

- `/analyze/:text` - To analyze the sentiment of the text passed. It returns positive, negative, or neutral.

The **"Dealerships Website"** consumes the **"Sentiment Analyzer Service"** to analyze the sentiments of the reviews through the Django Proxy contained within the Django application.
