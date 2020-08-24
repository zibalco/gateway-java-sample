
# Zibal Payment Gateway Java Code Sample

For this code sample we used JSON-java repository.
You can get the .jar file from here:
https://repo1.maven.org/maven2/org/json/json/20200518/json-20200518.jar

## Request payment sample
```java
private static HttpURLConnection connection;  
  
public static void main(String[] args) {  
    BufferedReader reader;  
  String line;  
  StringBuffer responseContent = new StringBuffer();  
  
  StringBuilder response = null;  
 try {  
        URL url = new URL("https://gateway.zibal.ir/v1/request");  
  connection = (HttpURLConnection) url.openConnection();  
  // Request setup  
  connection.setRequestMethod("POST");  
  connection.setRequestProperty("Content-Type", "application/json; utf-8");  
  connection.setRequestProperty("Accept", "application/json");  
  connection.setDoOutput(true);  
  String jsonInputString = "{" +  
                "\"merchant\": \"zibal\",\n" +  
                "\"amount\": 160000,\n" +  
                "\"callbackUrl\": \"http://yourapiurl.com/callback.php\"" +  
                "}";  
 try (OutputStream os = connection.getOutputStream()) {  
            byte[] input = jsonInputString.getBytes("utf-8");  
  os.write(input, 0, input.length);  
  }  
        try (BufferedReader br = new BufferedReader(  
                new InputStreamReader(connection.getInputStream(), "utf-8"))) {  
            response = new StringBuilder();  
  String responseLine = null;  
 while ((responseLine = br.readLine()) != null) {  
                response.append(responseLine.trim());  
  }  
        }  
        int status = connection.getResponseCode();  
  System.out.println(status);  
  
  
  } catch (MalformedURLException e) {  
        e.printStackTrace();  
  } catch (IOException e) {  
        e.printStackTrace();  
  }  
  
    // Parse response JSON into JSONObject  
  JSONObject result = new JSONObject(response.toString());  
  System.out.println(result.getString("message"));  
  
}

```
