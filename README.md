import org.json.JSONObject;
import org.json.JSONTokener;
import java.io.FileReader;
import java.math.BigInteger;
import java.util.HashMap;
import java.util.Map;

public class ShamirSecretSharing {

    public static void main(String[] args) {
        try {
            FileReader reader = new FileReader("input.json");
            JSONTokener tokener = new JSONTokener(reader);
            JSONObject jsonObject = new JSONObject(tokener);
            JSONObject keys = jsonObject.getJSONObject("keys");
            int n = keys.getInt("n");
            int k = keys.getInt("k");
            Map<Integer, BigInteger> points = new HashMap<>();
            for (String key : jsonObject.keySet()) {
                if (key.equals("keys")) continue;
                int x = Integer.parseInt(key);
                JSONObject pair = jsonObject.getJSONObject(key);
                String base = pair.getString("base");
                String value = pair.getString("value");
                BigInteger y = new BigInteger(value, Integer.parseInt(base));
                points.put(x, y);
            }
            
            BigInteger constantTerm = findConstantTerm(points, k);
            System.out.println("The secret constant term is: " + constantTerm);
            
        } catch (Exception e) {
            e.printStackTrace();
        }
    }
    
    public static BigInteger findConstantTerm(Map<Integer, BigInteger> points, int k) {
        return BigInteger.ZERO;
    }
}
