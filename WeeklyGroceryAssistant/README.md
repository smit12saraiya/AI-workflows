# Weekly Grocery Assistant - n8n Workflow

An intelligent n8n workflow that automates weekly meal planning and grocery list generation using AI-powered ingredient extraction.

## 🎯 Overview

This workflow helps you manage weekly meal planning by:
- Reading meal preferences from Google Sheets
- Using AI to generate detailed ingredient lists for selected meals
- Automatically updating your meal database with ingredients
- Sending weekly reminder emails to update meal plans
- Enriching meals with YouTube cooking videos

## 🏗️ Workflow Architecture

```
Manual Trigger → Google Sheets (Read) → Process Data → AI Ingredient Generation → Update Database with ingredients list and Youtube video
```

### Key Components:
1. **Google Sheets Integration** - Manages meal database and preferences
2. **AI-Powered Ingredient Generator** - Uses Claude 3.7 Sonnet via OpenRouter to extract ingredients
3. **Email Notifications** - Gmail integration for weekly reminders
4. **YouTube Enrichment** - Calls sub-workflow to add cooking videos

## 📋 Prerequisites

### Required n8n Credentials:
- **Google Sheets OAuth2** - For reading/writing meal data from your Google Sheets
- **OpenRouter API** - For AI-powered ingredient generation using Claude 3.7 Sonnet
- **Gmail OAuth2** - For sending weekly meal planning reminder emails

### Google Sheets Setup:
Create a Google Sheet with columns:
- `Meal Options` - Name of the dish
- `Include in Week` - Yes/No flag for weekly selection
- `Ingredients To Cook` - Auto-generated ingredient list
- `Servings` - Number of servings
- `Youtube Link` - Cooking video links (auto-populated)
- `row_number` - Unique identifier for each meal

## 🚀 Installation & Setup

### 1. Import Workflow
- Import the `Weekly Grocery Assistant.json` file into your n8n instance
- The workflow will appear as "Weekly Grocery Assistant"

### 2. Configure Credentials
Replace the following credential placeholders with your own:

#### Google Sheets OAuth2:
- Node: "Get row(s) in sheet", "Update Ingredients in Meals Database", "Reset the Sheet", "Fetch meal preferences"
- **Action Required**: Set up Google Sheets OAuth2 credentials in n8n

#### OpenRouter API:
- Node: "OpenRouter Chat Model"
- **Action Required**: Add your OpenRouter API key for Claude 3.7 Sonnet access

#### Gmail OAuth2:
- Node: "Send a message"
- **Action Required**: Configure Gmail OAuth2 for sending reminder emails

### 3. Update Configuration
- **Google Sheets Document ID**: Replace `1a9XpZ_AD-r0XcJMGZgEE99sTPx766kS5NdVjBwlgNB4` with your sheet ID
- **Email Recipients**: Update email addresses in "Send a message" node
- **YouTube Enrichment Workflow**: Ensure the sub-workflow is another n8n workflow which is expert in searching the youtube for specific item and returning the most liked video for the dish selected.

## 🔄 How It Works

### Workflow Process:
1. **Manual Trigger** - Start the workflow manually / or you can add scheduled trigger
2. **Read Meal Data** - Fetches all meals from Google Sheets
3. **Reset Previous Data** - Clears old ingredient data and resets flags
4. **Send Reminder Email** - Notifies users to update meal preferences
5. **Wait Period** - 30-second delay for manual updates
6. **Process Selected Meals** - Filters meals marked "Include in Week = Yes"
7. **AI Ingredient Generation** - Uses Claude 3.7 Sonnet to generate detailed ingredient lists
8. **Format Results** - Structures ingredients for grocery shopping
9. **YouTube Enrichment** - Adds cooking videos (optional sub-workflow)
10. **Update Database** - Saves generated ingredients back to Google Sheets

### AI Ingredient Generation Features:
- Scales ingredients based on servings
- Uses common grocery units (g, ml, pcs, tbsp, tsp, cup)
- Provides realistic quantities for shopping
- Formats ingredients in readable grocery list format
- Maintains consistency across ingredient naming

## 📧 Email Notifications

The workflow sends HTML-formatted reminder emails with:
- Weekly meal planning reminder
- Direct link to your Google Sheets
- Professional styling with emojis
- Automated scheduling capability

## 🛠️ Customization Options

### Modify AI Behavior:
Edit the system message in "Ingredient Generator Agent" to:
- Change ingredient formatting preferences
- Adjust quantity scaling logic
- Modify dietary restrictions or preferences

### Email Template:
Customize the HTML email template in "Send a message" node for:
- Different styling
- Additional recipients
- Custom reminder frequency

### Sheet Structure:
Adapt the Google Sheets column mapping in update nodes for:
- Different column names
- Additional meal metadata
- Custom data fields

## 🔧 Troubleshooting

### Common Issues:
1. **Credential Errors**: Ensure all OAuth2 credentials are properly configured
2. **Sheet Access**: Verify Google Sheets permissions for the service account
3. **AI Generation Fails**: Check OpenRouter API key and quota limits
4. **Email Not Sending**: Confirm Gmail OAuth2 scope includes email sending

### Debug Tips:
- Use n8n's execution log to trace data flow
- Test individual nodes before running full workflow
- Verify Google Sheets document ID and sheet names
- Check AI model availability on OpenRouter

## 📝 Usage Tips

1. **Weekly Routine**: Run workflow at the start of each week
2. **Meal Selection**: Mark desired meals with "Include in Week = Yes"
3. **Serving Adjustment**: Update serving counts before running workflow
4. **Grocery Shopping**: Use generated ingredient lists for shopping
5. **Recipe Videos**: Check YouTube links for cooking instructions

## 🤝 Contributing

Feel free to fork and customize this workflow for your needs. Common enhancements:
- Add nutrition calculation
- Integrate with grocery delivery APIs
- Include meal prep scheduling
- Add dietary restriction filtering

**Note for n8n Beginners**: This workflow requires setting up credentials (authentication) for Google Sheets, OpenRouter, and Gmail services. Each service needs to be connected once in n8n's credential manager before the workflow can access your data.
