# Temple Architecture AI - 3D Temple Generator

An advanced AI-driven platform that transforms ancient Sanskrit architectural texts into immersive, interactive 3D temple models, leveraging cutting-edge visualization and analysis technologies.

## Features

- Translate Sanskrit architectural texts to English using OpenAI's GPT-4o
- Generate realistic 3D temple models based on traditional styles (Dravidian, Nagara, Vesara, Kerala)
- Interactive 3D viewer with rotation, zooming, and panning
- Example showcase featuring detailed temple models
- Generator page for creating custom temple designs
- Library page to browse saved models
- Photorealistic rendering with advanced lighting and materials

## Technology Stack

- Frontend: React, TypeScript, Vite, TailwindCSS, shadcn/ui
- 3D Rendering: Three.js with advanced post-processing effects
- Backend: Node.js, Express
- API Integration: OpenAI for NLP and 3D model generation
- 3D Modeling: Advanced procedural generation with Three.js and Blender integration

## Setting up for Local Development

### Prerequisites

- Node.js 18+ and npm installed
- An OpenAI API key

### Installation

1. **Clone the repository**:

   After downloading the project from Replit, unzip it and navigate to the project directory:

   ```bash
   cd temple-architecture-ai
   ```

2. **Install dependencies**:

   ```bash
   npm install
   ```

3. **Configure environment variables**:

   Create a `.env` file in the root directory by copying the `.env.example` file:

   ```bash
   cp .env.example .env
   ```

   Then edit the `.env` file and add your OpenAI API key:

   ```
   OPENAI_API_KEY=your_openai_api_key_here
   ```

   > **Important**: You must have a valid OpenAI API key with access to the GPT-4o model. The translate and model generation features will not work without this.

   **Getting an OpenAI API Key**:
   
   1. Visit [OpenAI Platform](https://platform.openai.com/)
   2. Sign up or log in to your OpenAI account
   3. Navigate to the [API Keys section](https://platform.openai.com/api-keys)
   4. Click "Create new secret key"
   5. Give your key a name (e.g., "Temple Architecture AI")
   6. Copy the generated key (you won't be able to see it again)
   7. Paste it into your `.env` file as shown above

   **Verify API Access**:
   
   Make sure your OpenAI account has access to the GPT-4o model. New accounts may need to add credit to their account before getting access to the most powerful models. Visit [OpenAI's pricing page](https://openai.com/pricing) for more information.

4. **Configure the API URL for local development**:

   Open `client/src/lib/config.ts` and uncomment the local development line:

   ```typescript
   // For local development
   export const API_BASE_URL = 'http://localhost:5000';
   ```

5. **Install additional development dependencies**:

   ```bash
   npm install concurrently --save-dev
   ```

6. **For local development, you need to run both backend and frontend separately**:

   **Terminal 1** - Start the backend server:
   ```bash
   npm run dev
   ```
   This will start the Express server at http://localhost:5000.

   **Terminal 2** - Start the frontend development server:
   ```bash
   cd client
   npx vite --port 3000
   ```
   This will start the Vite development server at http://localhost:3000.

7. **Access the application**:

   For the complete application with API access:
   ```
   http://localhost:5000
   ```

   For frontend development with hot reloading:
   ```
   http://localhost:3000
   ```

   Note: When using the frontend server at port 3000, make sure the API_BASE_URL in `client/src/lib/config.ts` is set to 'http://localhost:5000'.

## Using Visual Studio Code

This project works best with VS Code and the following extensions:

1. **TypeScript/JavaScript Extensions**:
   - ESLint
   - Prettier - Code formatter
   - JavaScript and TypeScript Nightly

2. **React Extensions**:
   - ES7+ React/Redux/React-Native snippets
   - Simple React Snippets

3. **Three.js Development**:
   - glTF Tools
   - 3D Viewer

4. **Debugging Tools**:
   - Debugger for Chrome/Edge

## Project Structure

- `client/` - Frontend React application
  - `src/components/` - Reusable UI components
  - `src/lib/` - Utility functions and API integrations
  - `src/pages/` - Main page components
- `server/` - Backend Express server
  - `openai.ts` - OpenAI API integration for text translation and model generation
  - `routes.ts` - API endpoints
  - `storage.ts` - Data storage layer
- `shared/` - Shared code between frontend and backend
  - `schema.ts` - Type definitions and schemas
- `attached_assets/` - 3D models and other assets

## Working with 3D Models

The project uses Three.js for rendering 3D models. The main components for 3D rendering are:

- `client/src/components/three-viewer.tsx` - The main 3D viewer component
- `client/src/lib/meshyAIIntegration.ts` - Integration with advanced 3D model generation
- `client/src/lib/threeUtils.ts` - Utility functions for Three.js

When testing locally, you can use the example GLB model included in the `attached_assets/` directory.

## Troubleshooting

### API Errors

If you encounter errors when using features like "Translate" or "Generate Model":

1. **OpenAI API Key Issues**:
   - Verify that your `.env` file contains a valid OpenAI API key
   - Make sure you've restarted both servers after adding the API key
   - Check your OpenAI account has sufficient credit/quota
   - Confirm that your API key has access to the GPT-4o model
   - Check OpenAI's [status page](https://status.openai.com/) for any service outages

2. **API Error Messages**:
   - `"OpenAI API key is not configured"`: You need to add your API key to the `.env` file
   - `"Rate limit exceeded"`: You've exceeded your OpenAI rate limits. Wait a few minutes or increase your quota.
   - `"Error 429"`: Rate limiting or quota issues with your OpenAI account
   - `"Error 401"`: Invalid API key. Check that you've copied the full key without any extra spaces
   - `"Error 403"`: Permission denied. Your account might not have access to GPT-4o

3. **API URL and Server Issues**:
   - Confirm `client/src/lib/config.ts` has the API_BASE_URL set correctly:
   ```typescript
   export const API_BASE_URL = 'http://localhost:5000';
   ```
   - Ensure both servers are running (backend on port 5000, frontend on port 3000)
   - Check browser console (F12) for detailed error messages and network requests
   - Use the complete application URL (http://localhost:5000) which serves both frontend and backend together

4. **Testing API Connections**:
   - Test the API directly with curl to verify backend connectivity:
   ```bash
   curl -X POST http://localhost:5000/api/translate -H "Content-Type: application/json" -d '{"sanskritText":"Test text"}'
   ```

5. **Server Diagnostics**:
   - Check terminal for Express server output and error messages
   - Try restarting the servers after any configuration change
   - Verify that your network can reach the OpenAI API (no firewall issues)

### 3D Model Loading Issues

If 3D models fail to load or display incorrectly:

1. **Asset File Issues**:
   - Confirm the GLB model file exists in the `attached_assets/` folder
   - Verify the file path is correct in all references
   - Check the model file isn't corrupted by opening it in another 3D viewer

2. **Three.js Debugging**:
   - Look for specific Three.js errors in the browser console
   - Common issues include:
     - "CORS policy" errors: Check server configuration for proper headers
     - Memory issues: Very large models might need optimization
     - WebGL compatibility problems: Try a different browser or check hardware acceleration settings

3. **Performance Problems**:
   - If models load slowly or cause performance issues:
     - Try using smaller/optimized models for testing
     - Check if your device has adequate GPU capabilities
     - Close other resource-intensive applications and browser tabs

4. **General Fixes**:
   - Clear your browser cache
   - Try a different browser
   - Restart both servers
   - Check for JavaScript errors in the console that might interrupt loading