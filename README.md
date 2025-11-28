# Hospital CRM (PRO System)

## Local Setup
1. Install dependencies: `pip install -r requirements.txt`
2. Run MongoDB locally.
3. Run the app: `python app.py`
4. Go to http://127.0.0.1:5000

## Vercel Deployment Instructions
1. **Create a MongoDB Atlas Account** (Free tier).
2. **Get Connection String**: It looks like `mongodb+srv://user:pass@cluster.mongodb.net/dbname`.
3. **Deploy to Vercel**:
   - Import this repo.
   - Go to **Settings > Environment Variables**.
   - Add a new variable:
     - **Key**: `MONGO_URI`
     - **Value**: (Your MongoDB Atlas Connection String)
4. **Redeploy**: The app needs this variable to connect.
