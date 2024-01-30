# weatherapp
Web Based Weather App using OpenWeatherMap API



The following is Lambda Code for the Index.html file

Axios must be added in as a layer in AWS


    // Handler for AWS Lambda
    exports.handler = async (event) => {
        const axios = require('axios');

    // Replace with your OpenWeatherMap API key
    const apiKey = 'API_KEY_GOES_HERE';

    // Parse city from event query string parameters
    const city = event.queryStringParameters.city + '&units=imperial';

    const url = `https://api.openweathermap.org/data/2.5/weather?q=${city}&appid=${apiKey}`;

    try {
        const response = await axios.get(url);
        return {
            statusCode: 200,
            headers: {
                "Access-Control-Allow-Origin": "*", // Required for CORS support
                "Access-Control-Allow-Headers": "Content-Type"
            },
            body: JSON.stringify(response.data)
        };
    } catch (error) {
        console.log(error);
        return {
            statusCode: error.response.status,
            body: JSON.stringify(error.response.data)
        };
    }
    };
