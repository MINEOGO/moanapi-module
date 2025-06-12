--- moanapi-module-master/README.md
+++ moanapi-module-master/README.md
@@ -9,22 +9,32 @@
 
 ## Usage
 
-First, import and initialize the client with your API key. The client will automatically load all available API categories.
+First, import and initialize the client with your API key. It's conventional to name the client instance `moan`.
 
     import moanapi
 
     try:
-        client = moanapi.Client(api_key="YOUR_API_KEY")
+        moan = moanapi.Client(api_key="YOUR_API_KEY")
 
-        # Access dynamically loaded API modules
-        quote = client.utility.get_quote(category="anime")
+        # Get an anime quote
+        quote = moan.utility.get_quote(category="anime")
         print(quote['quote'])
 
-        user = client.roblox.get_user_info(user_id=261)
+        # Get Roblox user info
+        user = moan.roblox.get_user_info(user_id=261)
         print(f"Username: {user['data']['username']}")
         
-        image_data = client.generative.get_flux_image(prompt="a powerful cat wizard")
+        # Generate an image with AI
+        image_data = moan.generative.get_flux_image(prompt="a powerful cat wizard")
         print(f"Image URL: {image_data['image_url']}")
+
+        # Generate a rankcard (returns raw image bytes)
+        image_bytes = moan.generative.generate_rankcard(
+            username="Zlan", avatar="AVATAR_URL", current_xp=900, 
+            next_level_xp=1000, level=24, rank=1
+        )
+        with open("rankcard.png", "wb") as f:
+            f.write(image_bytes)
 
     except moanapi.APIError as e:
         print(f"An API error occurred: {e}")
