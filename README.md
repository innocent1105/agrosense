
# AgroSense Backend Setup Guide

This README provides step-by-step instructions for setting up
the Backend that powers the AgroSense mobile app. 
  
The API is responsible for receiving sensor data 
(e.g., temperature, humidity, soil moisture) and storing it 
in a MySQL database.

---


## 1. Set Up the MySQL Database

- Create a new database named `agrosense`.

### Create the `sensor_data` table:

| Column         | Type      | Description                           |
|----------------|-----------|---------------------------------------|
| `id`           | INT       | Primary key, auto-increment           |
| `temperature`  | FLOAT     | Temperature value from the sensor     |
| `humidity`     | FLOAT     | Humidity value from the sensor        |
| `soil_moisture`| FLOAT     | Soil moisture value from the sensor   |
| `timestamp`    | DATETIME  | Defaults to current timestamp         |

### Create the `users` table (for future user authentication):

| Column       | Type         | Description                          |
|--------------|--------------|--------------------------------------|
| `id`         | INT          | Primary key, auto-increment          |
| `name`       | VARCHAR(100) | Full name of the user                |
| `email`      | VARCHAR(100) | User's email address (must be unique)|
| `password`   | VARCHAR(255) | Hashed password                      |
| `created_at` | DATETIME     | Timestamp of account creation        |

> Passwords should be hashed using `password_hash()` in PHP for security.

---

## 2. Create the Project Folder Structure

Inside your PHP server root directory (e.g., `htdocs/agrosense-api/`), create the following structure:

---

## 3. Configure the Database Connection

- In `config.php`, define your database credentials.
- Connect to the MySQL database using `mysqli`.

---

## 4. Build the Sensor Data API Endpoint

- In `insert_data.php`:
  - Accept POST requests containing JSON data.
  - Extract values for `temperature`, `humidity`, and `soil_moisture`.
  - Sanitize inputs and insert them into the `sensor_data` table.
  - Return a JSON response for success or error.

---

## 5. (Optional) Create a Fetch Endpoint for Latest Data

- In `get_data.php`:
  - Query the most recent row from the `sensor_data` table.
  - Return the data as a JSON object.

---

## 6. Test the API Endpoints

- Use Postman or Curl to:
  - Send POST requests to `insert_data.php` with sample data.
  - (Optionally) Send GET requests to `get_data.php` to retrieve the latest entry.
- Confirm that the data is saved correctly in the database.

---

## 7. Connect the API to Your React Native App

- Use `fetch()` or `axios` to:
  - POST data from sensors to `insert_data.php`
  - GET data from `get_data.php` for dashboard display

---

## 8. Secure and Optimize for Production

- Enable CORS if your app and API run on different origins.
- Use HTTPS for secure communication.
- Add input validation and error handling.
- (Optional) Add authentication using API keys or JWTs.
- (Optional) Add logging and rate limiting if needed.

---

##  Notes

- This backend uses **plain PHP** (no frameworks).
- You can easily expand it to include more endpoints, authentication, and analytics features.

---

# AgroSense Frontend Setup Guide - Web App

1. Tech Stack
- React
- Axios
- Tailwind CSS / Daisy UI / Shadcn
- Chart.js / Recharts / Plotly
- Vite or Create React App - But Vite is simple though

## Folder Structure
/src
├── components/         # UI components (e.g. SensorCard, Chart)
├── pages/              # Page views (e.g. Dashboard, Login)
├── services/           # Axios API logic
├── App.jsx             # Routing and layout
└── index.js            # Entry point

## 6. Pages to Build

- Dashboard: Display charts and live readings.
- Login and Signup.
- Profile : Show user account details.
- Payment Wall Page




