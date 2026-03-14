# Wardrobe Recommendation System - Complete Setup Guide

## Overview
You now have a dynamic wardrobe management system with AI-powered recommendations. Here's everything you need to get it running.

---

## PART 1: LOCAL SETUP

### Prerequisites
- Python 3.8+
- An Anthropic API key (you likely already have this for your macro briefing project)
- A text editor or GitHub Desktop

### Step 1: Clone or Create a New Repo

**Option A: Create new repo for this project**
```bash
# Create new directory
mkdir wardrobe-advisor
cd wardrobe-advisor
git init

# Copy the files
# - wardrobe.json (your inventory)
# - wardrobe_advisor.py (the recommendation engine)
```

**Option B: Add to existing repo**
If you're adding this to your existing GitHub repo (where your macro briefing system lives):
```bash
# In your existing repo
mkdir wardrobe
cp wardrobe.json wardrobe/
cp wardrobe_advisor.py wardrobe/
```

### Step 2: Install Dependencies

```bash
pip install anthropic
```

That's it! The script only uses `anthropic` and built-in Python libraries.

### Step 3: Set Your API Key

```bash
export ANTHROPIC_API_KEY="your-api-key-here"
```

Or add it to your `.env` file (create one in your project root):
```
ANTHROPIC_API_KEY=your-api-key-here
```

### Step 4: Run the Advisor (Local)

**Interactive Mode:**
```bash
python wardrobe_advisor.py
```

This opens a chat interface where you can ask questions like:
- "What should I buy with $300 for summer?"
- "How do I replace my Jordan 4s?"
- "What would work well with my Stone Island zip-up?"

**Batch Mode (for specific season):**
```bash
python wardrobe_advisor.py summer2026
# or
python wardrobe_advisor.py fall2026
```

This generates a report with specific product recommendations.

---

## PART 2: UPDATING YOUR WARDROBE

### How to Add New Items

After you buy something, edit `wardrobe.json` and add a new entry to the `"clothing"` array:

```json
{
  "id": "shoe_003",
  "category": "shoes",
  "type": "sneaker",
  "name": "New Balance 1906",
  "color": "white",
  "brand": "New Balance",
  "material": "leather/mesh",
  "condition": "excellent",
  "pricePoint": "mid-accessible",
  "estimatedPrice": 140,
  "acquired": "2026-03-15",
  "notes": "Summer-appropriate lightweight sneaker"
}
```

Then commit to git:
```bash
git add wardrobe.json
git commit -m "Added New Balance 1906 white sneaker"
git push origin main
```

### How to Mark Items as Worn or Remove Them

Change the `"condition"` field to:
- `"worn-needs-replacement"` → Item is worn out
- `"sold"` → You got rid of it
- `"archived"` → You don't wear it anymore

Then the system will automatically flag those as gaps to fill.

---

## PART 3: GITHUB AUTOMATION (Optional but Recommended)

### Why GitHub?
- Version control of your wardrobe (track what you bought and when)
- Free hosting
- Can trigger automated emails/notifications
- Scalable to more features later

### Setup GitHub Repo

1. **Create new repo on GitHub.com**
   - Name: `wardrobe-advisor`
   - Description: "AI-powered wardrobe management system"
   - Public or Private (your choice)
   - Initialize with README

2. **Clone it locally**
   ```bash
   git clone https://github.com/yourusername/wardrobe-advisor.git
   cd wardrobe-advisor
   ```

3. **Add your files**
   ```bash
   cp wardrobe.json .
   cp wardrobe_advisor.py .
   
   # Create a .gitignore
   echo ".env
   __pycache__/
   *.pyc" > .gitignore
   
   # Create a README
   cat > README.md << 'EOF'
   # Wardrobe Advisor
   
   An AI-powered wardrobe management system using the Anthropic Claude API.
   
   ## Quick Start
   ```bash
   pip install anthropic
   export ANTHROPIC_API_KEY="your-key"
   python wardrobe_advisor.py
   ```
   EOF
   
   # Commit and push
   git add .
   git commit -m "Initial commit: wardrobe database and advisor"
   git push origin main
   ```

---

## PART 4: AUTOMATED RECOMMENDATIONS VIA GITHUB ACTIONS (Advanced)

### Create a GitHub Actions Workflow

Create `.github/workflows/monthly_recommendations.yml`:

```yaml
name: Monthly Wardrobe Recommendations

on:
  schedule:
    - cron: '0 9 1 * *'  # Run on 1st of each month at 9 AM UTC
  workflow_dispatch:  # Allow manual triggering

jobs:
  recommendations:
    runs-on: ubuntu-latest
    
    steps:
      - uses: actions/checkout@v3
      
      - name: Set up Python
        uses: actions/setup-python@v4
        with:
          python-version: '3.11'
      
      - name: Install dependencies
        run: pip install anthropic
      
      - name: Generate recommendations
        run: python wardrobe_advisor.py summer2026 > recommendations_output.txt
        env:
          ANTHROPIC_API_KEY: ${{ secrets.ANTHROPIC_API_KEY }}
      
      - name: Commit recommendations
        run: |
          git config user.name "Wardrobe Bot"
          git config user.email "bot@wardrobe-advisor.local"
          git add recommendations_output.txt
          git commit -m "Monthly recommendations generated"
          git push origin main
        continue-on-error: true  # Don't fail if there are no changes
```

### Setup GitHub Secrets

1. Go to your GitHub repo → Settings → Secrets and variables → Actions
2. Click "New repository secret"
3. Name: `ANTHROPIC_API_KEY`
4. Value: Your Anthropic API key
5. Click "Add secret"

Now the system will automatically generate recommendations monthly!

---

## PART 5: INTEGRATING WITH EMAIL (Gmail API)

You already have Gmail API set up for your macro briefing. We can send recommendations there too.

### Add Email Delivery to wardrobe_advisor.py

```python
# At the top of wardrobe_advisor.py, add:
import base64
from email.mime.text import MIMEText
from google.auth.transport.requests import Request
from google.oauth2.credentials import Credentials
from google_auth_oauthlib.flow import InstalledAppFlow
from google.auth import default as google_auth_default
import google.auth.exceptions

def send_recommendations_email(recommendations, recipient_email):
    """Send recommendations via Gmail API."""
    try:
        creds, _ = google_auth_default(scopes=['https://www.googleapis.com/auth/gmail.send'])
    except google.auth.exceptions.DefaultCredentialsError:
        print("Gmail not configured. Run: python wardrobe_advisor.py to use locally.")
        return
    
    message = MIMEText(recommendations)
    message['to'] = recipient_email
    message['subject'] = 'Your AI Wardrobe Recommendations'
    
    raw_message = base64.urlsafe_b64encode(message.as_bytes()).decode()
    send_message = {'raw': raw_message}
    
    service = build('gmail', 'v1', credentials=creds)
    service.users().messages().send(userId='me', body=send_message).execute()
    print(f"✓ Recommendations sent to {recipient_email}")
```

---

## PART 6: EXPANDING THE SYSTEM (Future Ideas)

Once you get comfortable, you can add:

### 1. **Outfit Generation**
```bash
python wardrobe_advisor.py outfits
# Suggests complete outfits from existing wardrobe
```

### 2. **Price Monitoring**
Track prices on your wishlist items and alert when they drop.

### 3. **Seasonal Rotation**
Automatically suggests what to wear based on weather.

### 4. **Deal Aggregation**
Scan SSENSE, Farfetch, Browns Fashion, Dover Street Market for deals matching your style.

### 5. **Styling Tips**
Generate outfit combinations and styling guides for pieces you own.

---

## PART 7: QUICK REFERENCE

### How to update your wardrobe:
1. Edit `wardrobe.json` with new items
2. `git add wardrobe.json`
3. `git commit -m "Added [item name]"`
4. `git push`

### How to get recommendations:
- **Interactive**: `python wardrobe_advisor.py`
- **Summer 2026**: `python wardrobe_advisor.py summer2026`
- **Fall 2026**: `python wardrobe_advisor.py fall2026`

### How to refresh the system with new wardrobe data:
In the interactive mode, just type `refresh` and it reloads from your JSON file.

---

## PART 8: YOUR IMMEDIATE ACTION ITEMS

1. ✅ **Choose where to store this** (local, GitHub, both)
2. ✅ **Run the advisor locally** with your API key to test it
3. ✅ **Ask for summer recommendations** using the interactive mode or `summer2026` batch mode
4. ✅ **Buy recommended items** and add them to wardrobe.json
5. ✅ (Optional) Set up GitHub repo and Actions workflow
6. ✅ (Optional) Configure Gmail integration for automated recommendations

---

## Troubleshooting

**"ModuleNotFoundError: No module named 'anthropic'"**
```bash
pip install anthropic
```

**"ANTHROPIC_API_KEY not found"**
```bash
export ANTHROPIC_API_KEY="your-key-here"
# or create a .env file with the key
```

**"wardrobe.json not found"**
Make sure both `wardrobe.json` and `wardrobe_advisor.py` are in the same directory.

**Changes to wardrobe.json not showing up**
Type `refresh` in the interactive mode to reload the file.

---

## Questions?

This system is designed to be:
- **Simple** to run locally
- **Extensible** (easy to add features)
- **Automated** (can run on GitHub Actions)
- **Privacy-first** (your data stays with you)

Start with interactive mode, get comfortable with recommendations, then add GitHub automation if you want.

Happy building! 🎯
