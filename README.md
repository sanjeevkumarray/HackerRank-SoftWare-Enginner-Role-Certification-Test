# HackerRank-SoftWare-Enginner-Role-Certification-Test


![Screenshot 2024-04-12 163301](https://github.com/sanjeevkumarray/HackerRank-SoftWare-Enginner-Role-Certification-Test/assets/53333326/3b3b35f7-7f1f-4799-b79b-27965ae16bac)


 # Question 1:
 
 # Maximixing the Final Element 
 
 ![image](https://github.com/sanjeevkumarray/HackerRank-SoftWare-Enginner-Role-Certification-Test/assets/53333326/bbe9d74b-662d-45cf-9a2e-7a2ed6d51797)


 ![image](https://github.com/sanjeevkumarray/HackerRank-SoftWare-Enginner-Role-Certification-Test/assets/53333326/76388a82-b7a9-4074-8c8f-4ba42639cd10)


 ![image](https://github.com/sanjeevkumarray/HackerRank-SoftWare-Enginner-Role-Certification-Test/assets/53333326/c1dc6b68-81c6-4e7d-b5f8-00fe603f5160)

 ![image](https://github.com/sanjeevkumarray/HackerRank-SoftWare-Enginner-Role-Certification-Test/assets/53333326/3fa69a40-d7ea-4052-b393-891b266823da)


# Solutions 

![image](https://github.com/sanjeevkumarray/HackerRank-SoftWare-Enginner-Role-Certification-Test/assets/53333326/0044aec8-6fdb-4c57-bc15-6b73b38784a9)

# 

class Result {

    /*
     * Complete the 'getMaxValue' function below.
     *
     * The function is expected to return an INTEGER.
     * The function accepts INTEGER_ARRAY arr as parameter.
     */

    public static int getMaxValue(List<Integer> arr) {
    // Write your code here
     Collections.sort(arr);
     if(arr.get(0)!=1){
         arr.set(0,1);
     }
     for(int i=1;i<arr.size();i++){
         if(arr.get(i)-arr.get(i-1)>1){
             arr.set(i,arr.get(i-1)+1);
         }
     }
     return arr.get(arr.size()-1);

    }

}



# Question 2:

# 2.Largest  Number of Orders.

![image](https://github.com/sanjeevkumarray/HackerRank-SoftWare-Enginner-Role-Certification-Test/assets/53333326/1287c6ce-bf58-42ad-9248-143a6c110931)


![image](https://github.com/sanjeevkumarray/HackerRank-SoftWare-Enginner-Role-Certification-Test/assets/53333326/3c32dda0-3a02-4766-8606-9859394242fd)



# Solutions 
![image](https://github.com/sanjeevkumarray/HackerRank-SoftWare-Enginner-Role-Certification-Test/assets/53333326/d9491e42-baed-4e7d-890b-3adde013cfc1)



 
 # 

  /*
 Enter your query here.
 */
  SELECT CUSTOMER_ID
   FROM (
    SELECT CUSTOMER_ID, COUNT(ID) AS order_count
    FROM ORDERS
    GROUP BY CUSTOMER_ID
    ORDER BY order_count DESC, CUSTOMER_ID ASC
) AS temp
LIMIT 1;





# Question 3:


# REST API: Products in Range



![1](https://github.com/sanjeevkumarray/HackerRank-SoftWare-Enginner-Role-Certification-Test/assets/53333326/09a4710d-ffbe-411b-8457-7152f5461a94)

![2](https://github.com/sanjeevkumarray/HackerRank-SoftWare-Enginner-Role-Certification-Test/assets/53333326/56302338-f54d-4f46-af75-f44cf4a19dce)

![3](https://github.com/sanjeevkumarray/HackerRank-SoftWare-Enginner-Role-Certification-Test/assets/53333326/5d487156-5a31-4be6-823e-422494e5a89d)

![4](https://github.com/sanjeevkumarray/HackerRank-SoftWare-Enginner-Role-Certification-Test/assets/53333326/2bde4a52-3816-4d05-987b-8529e5f280bb)

![5](https://github.com/sanjeevkumarray/HackerRank-SoftWare-Enginner-Role-Certification-Test/assets/53333326/67c04c5d-5a38-4139-9159-8a35b4aedc4c)





# Solutions 

# 


    class Result {
    /*
     * Complete the 'getProductsInRange' function below.
     *
     * URL for cut and paste
     * https://jsonmock.hackerrank.com/api/inventory?category=<category>&page=<pageNumber>
     *
     * The function is expected to return an Integer value.
     * The function accepts String category, Integer minPrice and Integer maxPrice as arguments.
     * 
     */
    public static int getProductsInRange(String category, int minPrice, int maxPrice)
    {
        int totalItemsInRange = 0;
        int currentPage = 1;
        int totalPages = Integer.MAX_VALUE; 
        while (currentPage <= totalPages) {
            String url = "https://jsonmock.hackerrank.com/api/inventory?category=" + category + "&page=" + currentPage;
            try {
                HttpURLConnection connection = (HttpURLConnection) new URL(url).openConnection();
                BufferedReader reader = new BufferedReader(new InputStreamReader(connection.getInputStream()));
                StringBuilder response = new StringBuilder();
                String line;
                while ((line = reader.readLine()) != null) {
                    response.append(line);
                }
                reader.close();
                JSONParser parser = new JSONParser();
                JSONObject jsonResponse = (JSONObject) parser.parse(response.toString());
                JSONArray data = (JSONArray) jsonResponse.get("data");
                totalPages = Integer.parseInt(jsonResponse.get("total_pages").toString());
                for (Object obj : data) {
                    JSONObject item = (JSONObject) obj;
                    double price = Double.parseDouble(item.get("price").toString());
                    if (price >= minPrice && price <= maxPrice) {
                        totalItemsInRange++;
                    }
                }
            } catch (MalformedURLException e) {
                e.printStackTrace();
            } catch (IOException e) {
                e.printStackTrace();
            } catch (org.json.simple.parser.ParseException e) {
                e.printStackTrace();
            }
            currentPage++;
        }

        return totalItemsInRange;
    }
}





