import com.fasterxml.jackson.core.JsonProcessingException;
import com.fasterxml.jackson.databind.ObjectMapper;

import java.util.HashMap;
import java.util.Map;

public class MapToFormattedString {

    public static void main(String[] args) {
        // Example map
        Map<String, Object> map = new HashMap<>();
        map.put(" Model", "mistral");
        map.put(" Index", 3);

        // Convert map to the desired formatted string
        String formattedString = convertMapToFormattedString(map);
        
        // Print the final formatted string
        System.out.println(formattedString);
    }

    public static String convertMapToFormattedString(Map<String, Object> map) {
        ObjectMapper objectMapper = new ObjectMapper();
        try {
            // Convert the map to a JSON string
            String jsonString = objectMapper.writeValueAsString(map);

            // Escape the quotes in the JSON string
            String escapedString = jsonString.replace("\"", "\\\"");

            // Split the string into two parts and add the "+" for concatenation
            String part1 = escapedString.substring(0, escapedString.indexOf("\\\" Index"));
            String part2 = escapedString.substring(escapedString.indexOf("\\\" Index"));

            // Return the final formatted string with a plus sign in between
            return "\"" + part1 + "\" + \"" + part2 + "\"";
        } catch (JsonProcessingException e) {
            e.printStackTrace();
            return null;
        }
    }
}
