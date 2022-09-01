# Dynamic-Alts
Dynamic-Alts docs



org.apache.http example

        // get list of accounts by id

            CloseableHttpClient client = HttpClientBuilder.create().build();
		HttpPost post = new HttpPost("http://api.dynamic-alts.com/api/v1/accounts");
		post.setHeader("Content-Type", "application/json");
		post.setHeader("Accept", "application/json");
		post.setHeader("Accept-Charset", "UTF-8");
		JsonObject obj = new JsonObject();
		obj.addProperty("api-token", "your token");
		StringEntity entity = new StringEntity(GSON.toJson(obj));
		post.setEntity(entity);
		final JsonObject json = new JsonParser().parse(EntityUtils.toString(client.execute(post).getEntity())).getAsJsonObject();
		JsonArray accounts = json.get("accounts").getAsJsonArray(); // list of all accounts

        // int id
        // String name
        // String uuid (UUID.fromString(jsonObject.get("uuid").getAsString());)


        // get access token of the account

        public static String getAuthToken(int id) throws Throwable {
            CloseableHttpClient client = HttpClientBuilder.create().build();
            HttpPost post = new HttpPost("http://api.dynamic-alts.com/api/v1/login");
            post.setHeader("Content-Type", "application/json");
            post.setHeader("Accept", "application/json");
            post.setHeader("Accept-Charset", "UTF-8");
            JsonObject obj = new JsonObject();
            obj.addProperty("api-token", "your token");
            obj.addProperty("id", id);
            StringEntity entity = new StringEntity(GSON.toJson(obj));
            post.setEntity(entity);
            post.setHeader("Content-type", "application/json");
            String data = EntityUtils.toString(client.execute(post).getEntity());
            final JsonObject jsonObject = new JsonParser().parse(data).getAsJsonObject();
            String token = jsonObject.get("access_token").getAsString();
            return token;
	      }
