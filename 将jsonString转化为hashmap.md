// 将jsonString转化为hashmap

  private HashMap<String, Object> fromJson2Map(String jsonString) {

​    HashMap jsonMap = JSON.parseObject(jsonString, HashMap.class);

 

​    HashMap<String, Object> resultMap = new HashMap<String, Object>();

​    for(Iterator iter = jsonMap.keySet().iterator(); iter.hasNext();){

​      String key = (String)iter.next();

​      if(jsonMap.get(key) instanceof JSONArray){

​        JSONArray jsonArray = (JSONArray)jsonMap.get(key);

​        List list = handleJSONArray(jsonArray);

​        resultMap.put(key, list);

​      }else{

​        resultMap.put(key, jsonMap.get(key));

​      }

​    }

​    return resultMap;

  }

  private List<HashMap<String, Object>> handleJSONArray(JSONArray jsonArray){

​    List list = new ArrayList();

​    for (Object object : jsonArray) {

​      JSONObject jsonObject = (JSONObject) object;

​      HashMap map = new HashMap<String, Object>();

​      for (Map.Entry entry : jsonObject.entrySet()) {

​        if(entry.getValue() instanceof JSONArray){

​          map.put((String)entry.getKey(), handleJSONArray((JSONArray)entry.getValue()));

​        }else{

​          map.put((String)entry.getKey(), entry.getValue());

​        }

​      }

​      list.add(map);

​    }

​    return list;

  }