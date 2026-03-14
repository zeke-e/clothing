# How to Use Your Wardrobe Advisor in a Claude Project

This is the easiest way to shop for clothes with Claude knowing everything about you. Here's exactly how to set it up.

---

## STEP 1: Create a Claude Project

1. Go to **claude.ai**
2. Click the **Projects** icon in the left sidebar
3. Click **+ New Project**
4. Name it: **"Wardrobe Advisor"**
5. Description: "AI-powered personal styling and shopping recommendations"
6. Click **Create**

---

## STEP 2: Add the Project Instructions

1. Open your new Wardrobe Advisor project
2. Click the **⚙️ Settings** button (top right)
3. Look for **"Custom Instructions"** or **"Project Instructions"**
4. Copy the entire contents of `CLAUDE_PROJECT_INSTRUCTIONS.md` (the file I just created)
5. Paste it into the instructions field
6. Click **Save**

**What this does**: Tells Claude how to analyze your wardrobe, understand your style, and make smart recommendations.

---

## STEP 3: Upload Your Wardrobe File

Now you're ready to start using it!

1. In your Wardrobe Advisor project, start a new chat
2. Click the **📎 Attach** button (or drag/drop)
3. Select your `wardrobe.json` file
4. Type a message like:
   ```
   I've uploaded my wardrobe inventory. Let's look at what I have 
   and then talk about what I should buy for summer 2026 with my $300 budget.
   ```
5. Hit send

Claude will:
- ✅ Analyze your entire wardrobe
- ✅ Identify gaps and opportunities
- ✅ Suggest specific products
- ✅ Reference what you already own
- ✅ Give price ranges and where to buy

---

## STEP 4: Have Conversations About Shopping

### Example conversations:

**"What should I buy with $300 for summer?"**
Claude analyzes your file and gives you specific recommendations with brands, prices, and why each piece works.

**"I'm looking for shorts for summer"**
Claude suggests 2-3 specific options that coordinate with your existing pieces.

**"How would this pair with my Stone Island zip-up?"**
Upload an image or describe a piece, and Claude explains if it fits your aesthetic.

**"Replace my worn Jordan 4s"**
Claude suggests replacement sneakers that match your style and price point.

**"I just bought [new item]"**
You can tell Claude about your purchase verbally, or upload the updated wardrobe.json.

---

## STEP 5: Keep It Updated (Super Easy)

Whenever you buy something new:

### Option A: Tell Claude Verbally
```
"I just bought a New Balance 1906 in white for $140. 
Can you help me think about what else to prioritize?"
```
Claude will remember this in that conversation and adjust recommendations.

### Option B: Update the File and Upload
1. Add the new item to your `wardrobe.json` file
2. In your chat, upload the updated file
3. Say: "I've updated my wardrobe. Here are my new items..."
4. Claude re-analyzes and adjusts recommendations

**Preferred method**: Option A for quick updates, Option B when you want a full re-analysis.

---

## STEP 6: Organize Your Conversations

You'll probably have multiple conversations:
- "Summer Shopping - $300 Budget"
- "Replacement Items Discussion"
- "Fall 2026 College Prep"
- "Styling Tips"
- etc.

Claude will remember the full context of your wardrobe file within each project conversation, so you can always reference what you own.

---

## Example Workflow

### First Time:
```
You: [Upload wardrobe.json]
"Hey, I'm preparing for college and need to upgrade my wardrobe. 
I have $300 for summer. What should I prioritize?"

Claude: [Analyzes file]
"Great wardrobe foundation! I see you have [analysis]. 
For summer with $300, I recommend:
1. New Balance 1906 White - $140 (pairs with your black GATs)
2. ALD Linen Shirt Cream - $95
3. Beckett Simonon Chino Shorts - $65
..."
```

### After Shopping:
```
You: "I bought the New Balance and the ALD linen shirt. 
Now I have $65 left. What's the best way to use it?"

Claude: [Remembers your purchases from conversation]
"With $65 left, you have options:
- Beckett Simonon shorts (perfect with new sneaker)
- Uniqlo lightweight shirt (accessible backup)
- Save for fall budget..."
```

### Next Season:
```
You: [Upload updated wardrobe.json with new items]
"Updated my wardrobe! Now planning for fall 2026 with $500. 
I'll be at college, so what do I need?"

Claude: [Fresh analysis with new inventory]
"Perfect! Now that you have [new pieces], for fall I recommend:
1. ALD Crewneck Sweater...
2. Stone Island Overshirt...
..."
```

---

## Pro Tips

### 1. **Create Conversation Bookmarks**
As you build collections of advice, take screenshots or save important recommendations.

### 2. **Use Clear Naming**
Name your project conversations clearly:
- ✓ "Summer 2026 Shopping"
- ✓ "Fall College Prep - $500"
- ✓ "Replacement Items"
- ✗ "Chat 1", "Wardrobe Talk"

### 3. **Reference Existing Pieces**
Always ask Claude about coordination:
- "How does this work with my Fugazi jeans?"
- "Would this clash with my Moncler crew?"

### 4. **Get Specific Recommendations**
Don't ask "What should I buy?" Ask:
- "What lightweight pants would work for summer?"
- "What's a good replacement for my worn Jordan 4s?"
- "I have $150 left. What's the highest impact piece?"

### 5. **Mix Seasons**
If you're planning ahead, upload your wardrobe and say:
- "Planning for fall 2026 (5 months from now)"
- Claude will factor in your current pieces + college lifestyle

---

## File Format

Your `wardrobe.json` includes:
- ✅ Everything you own with details
- ✅ Your style profile
- ✅ Your budget breakdown
- ✅ Gaps to fill (by season)
- ✅ Brand preferences
- ✅ Condition of items (what needs replacing)

Claude can read all of this automatically when you upload the file.

---

## Updating Your Wardrobe.json

When you buy something, add it to the JSON:

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
  "notes": "Summer sneaker for lighter outfits"
}
```

Then upload the updated file to your Claude Project conversation.

---

## What Claude Will Do Automatically

Once you have the instructions set up:

✓ **Analyze your wardrobe** - Understand what you own, value, and style
✓ **Identify gaps** - Know what's missing or needs replacement
✓ **Make specific recommendations** - Actual products, not generic advice
✓ **Reference your pieces** - "This works with your Stone Island zip"
✓ **Consider budget** - Stay within your $300/$500 allocation
✓ **Factor in seasonality** - Summer vs fall needs
✓ **Think about college** - Recommend versatile, durable pieces for dorm life
✓ **Suggest where to buy** - SSENSE, Browns Fashion, brand sites, etc.

---

## Quick Command Reference

| What You Want | How to Ask |
|---|---|
| Summer recommendations | "Analyze my wardrobe and suggest summer pieces" |
| Fall prep | "I'm going to college in fall. What should I buy?" |
| Replacement item | "My Jordan 4s are worn. What should I replace them with?" |
| Budget optimization | "I have $X left. What's the best way to use it?" |
| Coordination advice | "Would [item] work with my [existing piece]?" |
| Price guidance | "What should I expect to spend on [type of item]?" |
| Brand recommendations | "What other brands should I explore?" |
| Styling tips | "How can I style my [item] multiple ways?" |

---

## Troubleshooting

**"Claude isn't analyzing my file"**
- Make sure your wardrobe.json is properly formatted (valid JSON)
- Upload it fresh in the message
- Give Claude explicit instructions: "Here's my wardrobe file. Let's discuss..."

**"Claude forgot what I told it earlier"**
- Claude remembers within each conversation
- If you start a new chat, upload your file again
- Consider keeping all wardrobe discussions in one project conversation

**"I want to start fresh"**
- Create a new conversation in the same project
- Upload your updated wardrobe.json
- Proceed as normal

**"The file is too complex"**
- The JSON structure I created is designed for Claude to parse
- If there's an issue, simplify by removing older items or archiving them

---

## Next Steps

1. ✅ Create the Claude Project
2. ✅ Copy-paste the project instructions
3. ✅ Upload your wardrobe.json
4. ✅ Have your first conversation!

**That's it.** You now have an AI personal stylist that knows everything about you and can help you shop smartly.

---

## Future Enhancements (Optional)

Once you're comfortable, you can:
- **Ask for outfit combinations** from existing pieces
- **Share photos** of items you're considering
- **Get styling tips** for pieces you already own
- **Explore new brands** in your aesthetic
- **Save conversations** as shopping guides

But the core setup is complete now. Start shopping! 🎯
