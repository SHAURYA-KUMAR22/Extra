import com.fasterxml.jackson.core.JsonProcessingException;
import com.fasterxml.jackson.databind.ObjectMapper;

import java.util.HashMap;
import java.util.Map;

public class MapToJsonConverter {

    public static void main(String[] args) {
        // Example map
        Map<String, Object> map = new HashMap<>();
        map.put("Model", "mistral");
        map.put("Index", 3);

        // Convert the map to a JSON string
        String jsonString = convertMapToJsonString(map);
        
        // Print the JSON string
        System.out.println(jsonString);
    }

    public static String convertMapToJsonString(Map<String, Object> map) {
        ObjectMapper objectMapper = new ObjectMapper();
        try {
            // Convert the map to JSON string
            return objectMapper.writeValueAsString(map);
        } catch (JsonProcessingException e) {
            e.printStackTrace();
            return null;
        }
    }
}
