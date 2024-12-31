# StartupAid

## Description

StartupAid is a web application designed to help startups collect valuable feedback from their users. It provides a streamlined and efficient way to create, distribute, and analyze surveys, enabling startups to make data-driven decisions and improve their products or services.

This project was built using **Node.js**, **Express**, **React**, **Redux**, **MongoDB**, and utilizes **SendGrid** for email delivery and **Stripe** for payment processing. It was bootstrapped with [Create React App](https://github.com/facebook/create-react-app).

## Features

-   **User Authentication:** Secure user authentication via Google OAuth 2.0.
-   **Survey Creation:** Intuitive form for creating surveys with customizable title, subject, body, and recipient list.
-   **Email Distribution:** Integrates with SendGrid to send surveys to a list of recipients via email.
-   **Payment Processing:** Uses Stripe to allow users to purchase email credits for sending surveys.
-   **Survey Responses:** Tracks and displays 'yes' and 'no' responses for each survey.
-   **Dashboard:** Provides a dashboard to view a list of created surveys and their response statistics.
-   **Responsive Design:** Optimized for desktop and mobile devices.
-   **Production-Ready:** Built with best practices for deployment to production environments (e.g., Heroku).

## Table of Contents

-   [Getting Started](#getting-started)
    -   [Prerequisites](#prerequisites)
    -   [Installation](#installation)
-   [Usage](#usage)
    -   [Development](#development)
    -   [Production](#production)
-   [API Documentation](#api-documentation)

## Getting Started

These instructions will get you a copy of the project up and running on your local machine for development and testing purposes.

### Prerequisites

-   **Node.js:** Ensure you have Node.js installed (version 13.0.1 or higher recommended). You can download it from [nodejs.org](https://nodejs.org/).
-   **npm/Yarn:** This project uses `yarn` as the package manager. You can install it via `npm install -g yarn`.
-   **MongoDB:** You'll need a MongoDB database. You can either set up a local MongoDB instance or use a cloud-based solution like MongoDB Atlas.
-   **Google OAuth 2.0 Credentials:** Obtain a Client ID and Client Secret from the Google Developer Console.
-   **Stripe API Keys:** Get your Stripe Publishable Key and Secret Key from your Stripe dashboard.
-   **SendGrid API Key:** You'll need a SendGrid API key to send emails.

### Installation

1. **Clone the repository:**

    ```bash
    git clone https://github.com/rohanbpatel14/StartupAid.git
    cd StartupAid
    ```

2. **Install server dependencies:**

    ```bash
    yarn install
    ```

3. **Install client dependencies:**

    ```bash
    cd client
    yarn install
    cd ..
    ```

4. **Set up environment variables:**

    -   Create a `.env` file in the root directory of the project.
    -   Add the following environment variables to the `.env` file, replacing the placeholders with your actual credentials:

    ```
    GOOGLE_CLIENT_ID=your_google_client_id
    GOOGLE_CLIENT_SECRET=your_google_client_secret
    MONGO_URI=your_mongodb_connection_string
    COOKIE_KEY=your_cookie_key
    STRIPE_PUBLISHABLE_KEY=your_stripe_publishable_key
    STRIPE_SECRET_KEY=your_stripe_secret_key
    SEND_GRID_KEY=your_sendgrid_api_key
    REDIRECT_DOMAIN=http://localhost:3000 # Or your production domain
    ```

    -   In the `client` directory create two files `.env.development` and `.env.production` and add the following environment variable:
    ```
    REACT_APP_STRIPE_KEY=your_stripe_publishable_key
    ```

    **Note:** The `COOKIE_KEY` can be any random string used to encrypt the cookie.

## Usage

### Development

To run the application in development mode, use the following command:

```bash
yarn dev
```

This will start both the backend server (on port 5000) and the React development server (on port 3000) concurrently. Open [http://localhost:3000](http://localhost:3000) to view the application in your browser.

### Production

1. **Build the React application:**

    ```bash
    cd client
    yarn build
    cd ..
    ```

    This will create a `build` folder inside the `client` directory, containing the production-ready static files.

2. **Start the server:**

    ```bash
    yarn start
    ```

    This will start the Node.js server, which will also serve the built React application.

    **Note:** Ensure that the `NODE_ENV` environment variable is set to `production` in your production environment.

## API Documentation

### Authentication

-   **`/auth/google` (GET):** Initiates Google OAuth 2.0 authentication.
-   **`/auth/google/callback` (GET):** Callback URL for Google OAuth 2.0.
-   **`/api/logout` (GET):** Logs out the current user.
-   **`/api/current_user` (GET):** Returns the currently logged-in user.

### Billing

-   **`/api/stripe` (POST):** Handles Stripe payments for purchasing email credits. Requires authentication.

### Surveys

-   **`/api/surveys` (GET):** Retrieves all surveys created by the logged-in user. Requires authentication.
-   **`/api/surveys` (POST):** Creates a new survey. Requires authentication and sufficient email credits.
-   **`/api/surveys/:surveyId/:choice` (GET):** Records a user's response to a survey (yes/no).
-   **`/api/surveys/webhooks` (POST)**: Receives and processes webhook events from SendGrid, specifically for tracking user interaction with the survey emails.