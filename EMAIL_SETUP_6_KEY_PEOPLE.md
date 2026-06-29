# Keith-Otter Email Integration - 6 Key People

## ✅ ENABLED: Email Filtering for Key People

The system now pulls emails from **your 6 key people** and includes them in your daily briefing!

### Key People (Top Priority)
1. **Kevin**
2. **Cristina**
3. **Otter**
4. **Fortunfoods**
5. **Edd**
6. **Attio**

---

## 🚀 Quick Setup

### Step 1: Get Gmail API Credentials
1. Go to [Google Cloud Console](https://console.cloud.google.com)
2. Create a new project (or use existing)
3. Enable **Gmail API**
4. Create **OAuth 2.0 Desktop Application** credentials
5. Download JSON file as `credentials.json`
6. Place in repository root: `credentials.json`

### Step 2: First Authentication
```bash
python scripts/fetch_emails.py
```
- Opens browser for Google authorization
- Saves token for future runs
- Automatically fetches emails from your 6 key people

### Step 3: Test Locally
```bash
# Fetch emails
python scripts/fetch_emails.py

# Check output
cat agenda/emails.json

# Build full briefing
python scripts/build_agenda.py

# View result
cat agenda/briefing.md
```

---

## 📧 Daily Briefing Output Example

```markdown
# Daily Briefing - 2026-06-29

## 📧 Important Emails (Key People)

### **Kevin**
**Project Alpha: Ready for Review**
_Just completed the milestone. All tests passing. Ready for your approval..._

### **Cristina**
**Q3 Budget Approval Needed**
_We need to finalize the budget allocation by EOD. See attached spreadsheet..._

### **Otter**
**Weekly Sync - Action Items**
_Following up on last week's discussion. We have 3 items to complete..._

### **Fortunfoods**
**Partnership Opportunity**
_Potential new client wants to discuss integration. Available next Tuesday?..._

### **Edd**
**Infrastructure Alert**
_Performance metrics showing spike. Investigating now. Will update in 1 hour..._

### **Attio**
**CRM Data Update**
_Customer records have been synced. 450 new leads processed..._

## 📅 Today's Schedule
- 09:00: Team Standup
- 14:00: 1:1 with Manager

## 📰 Top Stories
1. [New Python Release](https://python.org)
2. [Cloud Infrastructure News](https://news.example.com)
```

---

## ⚙️ Configuration

### Edit `config.json`
```json
{
  "include_emails": true,
  "key_people": [
    "Kevin",
    "Cristina",
    "Otter",
    "Fortunfoods",
    "Edd",
    "Attio"
  ]
}
```

### Modify `scripts/fetch_emails.py`
```python
VIP_SENDERS = {
    "kevin@company.com": "Kevin",
    "cristina@company.com": "Cristina",
    "otter@company.com": "Otter",
    "fortunfoods@company.com": "Fortunfoods",
    "edd@company.com": "Edd",
    "attio@company.com": "Attio",
}
```

---

## 🔄 How It Works

### Daily Workflow
```
6:00 AM UTC Trigger
    ↓
fetch_rss.py (news/articles)
    ↓
fetch_emails.py (emails from Kevin, Cristina, etc.)
    ↓
fetch_calendar.py (today's events)
    ↓
build_agenda.py (combines all into briefing)
    ↓
text_to_speech.py (generates audio)
    ↓
Commit & Push to repo
```

### What Gets Fetched
- ✅ **Unread emails only** from your 6 key people
- ✅ **Latest 1 email per person** (top priority)
- ✅ **Subject line and preview** (first 200 chars)
- ✅ **Sender name** (clearly identified)
- ✅ **Timestamp** (when email was sent)

---

## 🔐 Security & Privacy

✅ **Secure Authentication**
- Uses OAuth 2.0 (never stores passwords)
- Credentials saved as `credentials.json` (in .gitignore)
- Token auto-refreshes for 365 days

✅ **Data Privacy**
- Only reads emails (no modifications)
- Email snippets truncated (200 chars max)
- Local caching only (no external storage)
- Unread emails only (prevents stale data)

✅ **GitHub Security**
- `credentials.json` NOT committed to repo
- Protected by `.gitignore`
- Can optionally store as GitHub Secret for CI/CD

---

## 🧪 Testing

### Test Email Fetch
```bash
python scripts/fetch_emails.py
```

**Expected Output:**
```
============================================================
📧 Keith-Otter: Fetch VIP Emails
============================================================

Key People: Kevin, Cristina, Otter, Fortunfoods, Edd, Attio

✓ Gmail authenticated

🔍 Searching for emails from 6 key people...

  📧 Kevin             ✓ (2 email(s))
  📧 Cristina          ✓ (1 email(s))
  📧 Otter             (no unread emails)
  📧 Fortunfoods       ✓ (1 email(s))
  📧 Edd               ✓ (2 email(s))
  📧 Attio             (no unread emails)

✓ Saved 6 key emails to agenda/emails.json

✅ Found 6 important email(s)
============================================================
```

### View Emails JSON
```bash
cat agenda/emails.json
```

### Build Full Briefing
```bash
python scripts/build_agenda.py
```

### View Briefing
```bash
cat agenda/briefing.md
```

---

## 🆘 Troubleshooting

### "credentials.json not found"
**Solution:** 
1. Go to [Google Cloud Console](https://console.cloud.google.com)
2. Create OAuth 2.0 Desktop Application credentials
3. Download and save as `credentials.json` in project root

### "No emails found"
**Possible causes:**
- No unread emails from those 6 people
- Email addresses don't match (check spelling)
- Gmail not authorized
- Try: `python scripts/fetch_emails.py` to re-authenticate

### "Gmail auth failed"
**Solution:**
1. Delete `token.json` if it exists
2. Re-run: `python scripts/fetch_emails.py`
3. Authorize in browser popup

### "Gmail API not enabled"
**Solution:**
1. Go to [Google Cloud Console](https://console.cloud.google.com)
2. Select your project
3. Click "Enable APIs and Services"
4. Search for "Gmail API"
5. Click "Enable"

---

## 📱 What Your Briefing Looks Like

### Before (Without Emails)
```
## 📰 Top Stories
1. News article
2. Another article
```

### After (With Key People Emails) ✨
```
## 📧 Important Emails (Key People)

### **Kevin**
**Project Status Update**
_Ready for your review. All tests passing..._

### **Cristina**  
**Budget Approval**
_Need final sign-off by EOD..._

[More from Otter, Fortunfoods, Edd, Attio]

## 📅 Today's Schedule
...

## 📰 Top Stories
...
```

---

## 🚀 Deploy to Production

### Steps:
1. ✅ Create `credentials.json` (Google Cloud Console)
2. ✅ Test locally: `python scripts/fetch_emails.py`
3. ✅ Merge branch to `main`
4. ✅ GitHub Actions runs at 6 AM UTC
5. ✅ Check `agenda/briefing.md` for results

### Monitor First Run:
- Go to Actions tab in GitHub
- Watch `daily_agenda.yml` workflow
- Check artifacts for briefing output
- Review `agenda/briefing.md` for emails

---

## 📞 Support

**Questions?** Check:
- [EMAIL_FILTERING_GUIDE.md](EMAIL_FILTERING_GUIDE.md) - Advanced filtering
- [SETUP_GUIDE.md](SETUP_GUIDE.md) - Full setup instructions
- [EMAIL_INTEGRATION.md](EMAIL_INTEGRATION.md) - Integration details

---

**Status:** ✅ Ready to Deploy  
**Key People:** Kevin, Cristina, Otter, Fortunfoods, Edd, Attio  
**Auto-run:** Daily at 6:00 AM UTC  
**Briefing Location:** `agenda/briefing.md`
