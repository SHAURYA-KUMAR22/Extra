import com.fasterxml.jackson.core.JsonProcessingException;
import com.fasterxml.jackson.databind.ObjectMapper;

import java.util.HashMap;
import java.util.Map;
import java.util.Iterator;

public class MapToConcatenatedString {

    public static void main(String[] args) {
        // Example map with multiple key-value pairs
        Map<String, Object> map = new HashMap<>();
        map.put(" Model", "mistral");
        map.put(" Index", 3);
        map.put(" AnotherKey", "SomeValue");
        map.put(" Number", 123);
        map.put(" IsValid", true);

        // Convert map to the desired formatted string
        String formattedString = convertMapToConcatenatedString(map);
        
        // Print the final formatted string
        System.out.println(formattedString);
    }

    public static String convertMapToConcatenatedString(Map<String, Object> map) {
        StringBuilder result = new StringBuilder();
        ObjectMapper objectMapper = new ObjectMapper();
        Iterator<Map.Entry<String, Object>> iterator = map.entrySet().iterator();

        while (iterator.hasNext()) {
            Map.Entry<String, Object> entry = iterator.next();
            try {
                // Convert each key-value pair to JSON and escape quotes
                String jsonString = objectMapper.writeValueAsString(entry.getValue());

                // Append the key and value in the required format
                result.append("\"").append(entry.getKey()).append("\": ").append(jsonString);

                // If there are more entries, add " + " for concatenation
                if (iterator.hasNext()) {
                    result.append(" + ");
                }
            } catch (JsonProcessingException e) {
                e.printStackTrace();
            }
        }

        // Wrap the entire result in curly braces
        return "\"{" + result.toString() + "}\"";
    }
}
