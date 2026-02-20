# Advanced Prompt Generator

A web application that uses Google's Gemini API to transform basic prompts into advanced, detailed prompts for better AI interactions.

## 🌐 Live Demo

[View Live Application](your-deployment-url-here)

## Features

### 🎯 Core Functionality
- **Prompt Enhancement**: Converts simple prompts into comprehensive, detailed prompts
- **Real-time Processing**: Asynchronous API calls with visual loading feedback
- **Clean UI**: Minimalist design with smooth transitions and animations

### 🎨 User Experience
- **Auto-expanding Textarea**: Input field automatically adjusts to content size
- **Loading Spinner**: Animated gradient spinner during API processing
- **Inline Error Validation**: Red border and error messages for empty inputs
- **Focus-based Error Clearing**: Errors disappear when user clicks on the input
- **Response-only View**: Input and button hide after generation to focus on results
- **New Prompt Button**: Easy workflow to generate another enhanced prompt

### 🔄 Workflow
1. User enters a basic prompt in the textarea
2. Clicks "Generate" button
3. "Generate" button disappear, loading spinner appears
4. Enhanced prompt displays in output area
5. "Enhance New Prompt" and "Copy to Clipboard" buttons appear
6. Click to copy generated prompt to clipboard or start a new enhancement 

## Technology Stack

### Frontend
- **HTML5**: Semantic structure
- **CSS3**: Custom styling with animations
  - Gradient spinner animation
  - Smooth transitions
  - Responsive design
- **JavaScript (ES6+)**: 
  - Async/await for API calls
  - DOM manipulation
  - Event handling
  - Input validation

### Backend
- **Node.js**: Runtime environment
- **Express.js**: Web server framework
- **Google Generative AI SDK**: Gemini API integration
- **dotenv**: Environment variable management

## Project Structure

```
project/
├── public/
│   ├── index.html       # Main HTML structure
│   ├── style.css        # Styling and animations
│   └── script.js        # Frontend logic
├── server.js            # Express server + Gemini API integration
├── .env                 # Environment variables (API keys)
├── package.json         # Dependencies
└── README.md            # This file
```

## API Integration

### Gemini API

The app uses Google's Gemini 3.0 Flash Experimental model for prompt enhancement.

**Key Implementation Details:**
```javascript
const genai = new GoogleGenerativeAI(process.env.GEMINI_API_KEY);
const model = genai.getGenerativeModel({model: "gemini-3.0-flash-preview"});
const result = await model.generateContent(promptText);
```

### Request/Response Flow

1. **Client Request**
   - User input sent via POST to `/submit`
   - Body: `{ title: "user's prompt" }`

2. **Server Processing**
   - Validates input
   - Calls Gemini API with enhancement instruction
   - Returns enhanced prompt

3. **Client Response**
   - Displays enhanced prompt
   - Handles errors gracefully

## Key Features Explained

### Auto-expanding Textarea
- Uses `field-sizing: content` CSS property
- Automatically grows with content
- Max height of 300px with scroll overflow

### Loading Spinner
- Conic gradient animation (cyan to magenta)
- Appears when Generate button is hidden
- 4px thick ring with smooth rotation

### Error Handling
- **Empty Input**: Red border + error message in placeholder
- **Server Errors**: Displayed in response area
- **Network Errors**: Caught and displayed to user

### State Management
```javascript
//loading state ON
generate.disabled = true;
spinner.classList.add('visible');

//loading state OFF
generate.disabled = false;
spinner.classList.remove('visible');
```

## Design Decisions

### UI/UX Choices
- **Single-page Application**: No navigation required
- **Progressive Disclosure**: Show only relevant elements at each step
- **Immediate Feedback**: Visual indicators for all user actions
- **Error Recovery**: Clear, actionable error messages

### Performance Optimizations
- **Hardware-accelerated CSS**: GPU-powered animations
- **Debounced Validation**: Reduces unnecessary processing
- **Minimal DOM Manipulation**: Efficient state updates

## Technical Highlights

### Gradient Spinner Animation
Custom CSS conic gradient with smooth rotation:
```css
background: conic-gradient(
    from 0deg, 
    rgb(0, 157, 255),    /*Cyan*/
    rgb(255, 0, 255),    /*Magenta*/
    rgb(0, 157, 255)     /*Loop back*/
);
animation: spin 0.8s linear infinite;
```

### Dynamic Input Validation
```javascript
function showError(inputElement, message) {
    inputElement.style.border = "2px solid red";
    inputElement.placeholder = message;
    inputElement.classList.add('error-placeholder');
}
```

### Async API Communication
```javascript
const response = await fetch('/submit', {
    method: 'POST',
    headers: {'Content-Type': 'application/json'},
    body: JSON.stringify({ title: promptText})
});
```

## Browser Support

- Chrome/Edge (latest)
- Firefox (latest)
- Safari (latest)
- Modern browsers with ES6+ support

## Performance

- **Average Response Time**: 2-5 seconds (depends on API)
- **Client-side Validation**: Instant feedback
- **Optimized CSS**: Hardware-accelerated animations

## Dependencies

```json
{
  "@google/generative-ai": "^latest",
  "express": "^4.x.x",
  "dotenv": "^16.x.x"
}
```

## Future Enhancements

- [ ] Prompt history/saved prompts
- [ ] Multiple enhancement styles/tones
- [ ] Character count indicator
- [ ] Dark mode toggle
- [ ] Export enhanced prompts

## Security

- API keys secured via environment variables
- Input validation on both client and server
- No user data storage or tracking
- HTTPS encryption in production

---

**Built with <3**
