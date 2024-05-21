# Weather App

Weather App is a simple web application that allows users to check the current weather conditions of various cities.

## Installation

1. Clone the repository:
https://github.com/ansh2842/weather-app.git
2. Install dependencies: axios,express,cors,tailwind
   

## Usage

1. Run the server:

2. Open your web browser and go to `http://localhost:3000` to access the Weather App.

3. Enter the name of a city in the input field and click the search button to view its current weather conditions.

## API Usage

This Weather App utilizes the OpenWeatherMap API to fetch weather data for cities. To use the app, you'll need to obtain an API key from OpenWeatherMap. Replace the `API_KEY` variable in the `routes/index.js` file with your API key.

## Folder Structure

- `routes/index.js`: Express.js routes for handling weather data retrieval from the OpenWeatherMap API.
- `public/index.html`: HTML file for the Weather App's user interface.
- `public/style.css`: CSS file for styling the Weather App.
- `public/image/clouds-transparent-background-75.png`: Image used for displaying weather conditions.
- `app.js`: Main entry point for the Weather App server.

## Contributing

Contributions are welcome! Please follow the guidelines in [CONTRIBUTING.md](CONTRIBUTING.md) to contribute to this project.

## License

This project is licensed under the [MIT License](LICENSE).
