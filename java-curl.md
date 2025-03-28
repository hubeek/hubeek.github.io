# Java Curl

_Status: Published_
_Created: 2023-05-14 04:25:56_
_Tags: java, curl, url_

```
import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;
import java.net.HttpURLConnection;
import java.net.URL;

public class CurlExample {
    public static void main(String[] args) {
        try {
            // Create a URL object with the desired endpoint
            URL url = new URL("https://api.example.com/some-endpoint");

            // Open a connection to the URL
            HttpURLConnection connection = (HttpURLConnection) url.openConnection();

            // Set the request method (GET, POST, etc.)
            connection.setRequestMethod("GET");

            // Send the request and receive the response
            int responseCode = connection.getResponseCode();

            // Check if the request was successful (status code 200)
            if (responseCode == HttpURLConnection.HTTP_OK) {
                // Read the response
                BufferedReader reader = new BufferedReader(new InputStreamReader(connection.getInputStream()));
                String line;
                StringBuilder response = new StringBuilder();

                while ((line = reader.readLine()) != null) {
                    response.append(line);
                }

                // Close the reader
                reader.close();

                // Print the response
                System.out.println(response.toString());
            } else {
                System.out.println("Request failed with response code: " + responseCode);
            }

            // Disconnect the connection
            connection.disconnect();
        } catch (IOException e) {
            e.printStackTrace();
        }
    }
}
```