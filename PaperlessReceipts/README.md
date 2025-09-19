# 📸 ImageOCR - Telegram Receipt Processing Workflow

An automated n8n workflow that processes receipt images sent via Telegram, extracts text using Google Vision API, and stores structured data in Google Sheets.

## 🚀 What This Workflow Does

1. **Receives Images**: Listens for photo messages on Telegram
2. **Downloads Images**: Automatically downloads the highest quality image
3. **Extracts Text**: Uses Google Vision API for OCR (Optical Character Recognition)
4. **AI Processing**: Leverages AI to structure receipt data (restaurant name, items, prices, totals)
5. **Stores Data**: Automatically saves structured information to Google Sheets

## 🔧 Prerequisites

- n8n instance (cloud or self-hosted)
- Telegram Bot Token
- Google Vision API Key
- OpenRouter API Key (for AI processing)
- Google Sheets with OAuth2 access

## ⚙️ Setup Instructions

### 1. Credentials Configuration
**For n8n beginners**: Credentials are stored securely in n8n and need to be created once - replace the placeholder credential IDs in the workflow with your actual credential names.

#### Required Credentials:
- **Telegram API**: Create a bot via @BotFather and add the token
- **Google Vision API**: Enable Vision API in Google Cloud Console and create an API key
- **OpenRouter API**: Sign up at OpenRouter and get your API key
- **Google Sheets OAuth2**: Set up OAuth2 credentials for Google Sheets access

### 2. Environment Variables
Set the following environment variable in your n8n instance:
```
GOOGLE_VISION_API_KEY=your_google_vision_api_key_here
```

### 3. Google Sheets Setup
1. Create a new Google Sheet
2. Add headers: `restaurant_name`, `address`, `phone`, `date_time`, `items`, `subtotal`, `tax`, `total`, `metadata`
3. Update the Google Sheets node with your sheet ID

### 4. Workflow Import
1. Copy the workflow JSON
2. Import into your n8n instance
3. Update all credential references
4. Activate the workflow

## 📋 Workflow Nodes Breakdown

| Node | Purpose | Configuration Needed |
|------|---------|---------------------|
| **Telegram Trigger** | Listens for messages | Telegram Bot credentials |
| **LargestPhoto** | Selects highest quality image | No configuration |
| **Download Binary** | Downloads image file | Telegram Bot credentials |
| **Extract from File** | Converts to base64 | No configuration |
| **HTTP Request** | Calls Google Vision API | Environment variable for API key |
| **Text Extraction** | Processes OCR response | No configuration |
| **AI Agent** | Structures receipt data | OpenRouter credentials |
| **Append row in sheet** | Saves to Google Sheets | Google Sheets credentials |

## 🎯 Usage

1. Start a chat with your Telegram bot
2. Send a photo of a receipt
3. The workflow automatically:
   - Downloads the image
   - Extracts text using OCR
   - Processes data with AI
   - Saves structured information to Google Sheets

## 📊 Output Format

The workflow extracts and stores:
- Restaurant name and contact details
- Date and time of purchase
- Individual items with prices
- Subtotal, tax, and total amounts
- Additional metadata

## 🔍 Troubleshooting

- **Telegram not responding**: Check bot token and webhook configuration
- **OCR not working**: Verify Google Vision API key and quota
- **AI processing fails**: Check OpenRouter API key and model availability
- **Google Sheets error**: Ensure OAuth2 credentials are valid and sheet permissions are correct

## 🛠️ Customization

- **Change AI Model**: Update the OpenRouter Chat Model node with different models
- **Modify Output Schema**: Edit the Structured Output Parser for different data fields
- **Add More Databases**: Replace or add nodes for Notion, Airtable, or other databases
- **Image Filters**: Add conditions to process only specific image types

## 📝 Notes

- The workflow processes the highest quality image from Telegram
- AI processing uses GPT-4o via OpenRouter for best accuracy
- All sensitive data is handled securely through n8n credentials
- The workflow can be extended to handle multiple image types beyond receipts

## 🤝 Contributing

Feel free to fork this workflow and customize it for your needs. Share improvements and variations with the n8n community!

---

**Built with ❤️ using n8n automation platform**
