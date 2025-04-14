Okay, here is a Product Requirements Document (PRD) tailored for an AI agent tasked with building the YouTube Video Summarizer React Native Expo App.

---

**Product Requirements Document: YouTube Video Summarizer App**

**1. Introduction & Overview**

This document outlines the requirements for building a cross-platform (iOS, Android, Web/PWA) application using React Native Expo. The core functionality of the app is to accept YouTube video links, generate summaries using the Gemini Flash-Lite model, store these summaries, and provide text-to-speech (TTS) playback with user controls. The application should be production-ready, robust, user-friendly, and maintainable.

**2. Goals**

*   **G1:** Provide users with concise and accurate summaries of YouTube videos.
*   **G2:** Offer flexible summary options (type and length) to cater to different user needs.
*   **G3:** Enable convenient consumption of summaries through adjustable text-to-speech playback.
*   **G4:** Allow easy input of video links via pasting and direct sharing from the YouTube app.
*   **G5:** Maintain a history of generated summaries for user reference.
*   **G6:** Deliver a seamless and performant user experience across iOS, Android, and Web (as a PWA).
*   **G7:** Enable sharing of generated summaries with others.

**3. Target Audience**

Users who want to quickly understand the content of YouTube videos without watching them entirely, including students, researchers, professionals, and casual viewers looking for time efficiency.

**4. Functional Requirements**

**4.1. Video Link Input & Validation**

*   **FR1.1 Paste Link:** Users must be able to paste a YouTube video URL directly into a designated text input field on the main screen.
*   **FR1.2 Share-to-App:** Users must be able to share a YouTube video link directly from the native YouTube application (iOS/Android) or web browser into this app using the native "Share" functionality. This action should automatically populate the input field or directly trigger the summarization process initiation.
*   **FR1.3 Initial Client-Side Validation:** The app must perform an initial, non-blocking check on the client-side to ensure the input string likely contains `youtube.com` or `youtu.be`. This is a preliminary check for user feedback; comprehensive validation occurs on the backend.
*   **FR1.4 Backend Validation:** The backend must robustly validate the received URL, confirming it's a valid and accessible YouTube video link using `ytdlp-nodejs`. Handle cases like private videos, deleted videos, or invalid formats.

**4.2. Summary Generation**

*   **FR2.1 Core Summarization:** Upon receiving a valid YouTube link, the app must trigger a backend process to generate a summary.
*   **FR2.2 AI Model:** Summary generation must utilize the **Gemini Flash-Lite** model via its API.
*   **FR2.3 Summary Type Selection:**
    *   Users must be able to select the desired type of summary: `Brief`, `Detailed`, or `Key Point`.
    *   A default summary type of `Brief` must be pre-selected.
    *   The selected type must be sent to the backend to influence the Gemini prompt/generation process.
*   **FR2.4 Summary Length Selection:**
    *   Users must be able to select the desired length of the summary: `Short`, `Medium`, or `Long`.
    *   A default summary length of `Medium` must be pre-selected.
    *   The selected length must be sent to the backend to influence the Gemini prompt/generation process.
*   **FR2.5 Fetch Video Metadata:** The backend must attempt to fetch the video's `Title` and `Thumbnail URL` using `ytdlp-nodejs` *before or concurrently* with summary generation.
*   **FR2.6 Metadata Fetch Fallback:** Summary generation **must not fail** if the `Title` or `Thumbnail URL` cannot be retrieved. Default placeholders or an indication of missing data should be used in the display if necessary, but the summary generation itself should proceed if transcripts are available.
*   **FR2.7 Transcript/Caption Dependency:** The backend process relies on fetching video transcripts or captions via `ytdlp-nodejs`.
*   **FR2.8 Transcript Availability Fallback:** If a video lacks transcripts or captions, the backend must detect this. The app must clearly inform the user on the frontend that the video cannot be summarized due to the lack of available text data. No summary should be generated or stored in this case.
*   **FR2.9 Cancellation:** Users must have a clear way to cancel a summary generation request while it is in progress (e.g., a "Cancel" button visible during the loading/processing state). The cancellation action should abort the backend request if possible or prevent the result from being processed/displayed if the request already completed.

**4.3. Summary Display**

*   **FR3.1 Card Format:** Generated summaries must be displayed in a visually distinct card format.
*   **FR3.2 Card Content:** Each summary card must display the following information:
    *   Video Title (Fetched, or placeholder if unavailable)
    *   Video Thumbnail (Fetched, or placeholder if unavailable)
    *   Summary Text (Rendered from stored Markdown format)
    *   Summary Type (`Brief`, `Detailed`, or `Key Point`)
    *   Summary Length (`Short`, `Medium`, or `Long`)
    *   Read Aloud Button
    *   Share Button
    *   Delete Button
    *   Edit Button
*   **FR3.3 Markdown Rendering:** The `Summary Text` must be stored in Markdown format and rendered correctly within the app (supporting basic formatting like paragraphs, lists, bold/italics if provided by Gemini).

**4.4. Text-to-Speech (TTS)**

*   **FR4.1 Read Aloud Functionality:** A "Read Aloud" button must be present on each summary card. Tapping this button initiates TTS playback of the `Summary Text`.
*   **FR4.2 Playback Control:** Basic playback controls (Play/Pause) must be available once TTS is initiated.
*   **FR4.3 Speed Adjustment:** Users must be able to adjust the playback speed of the TTS.
    *   Control: Provide a slider or stepper mechanism.
    *   Range: Allow speeds from 0.5x up to 16x the normal speed.
    *   Default: Normal speed (1x).
    *   Persistence: Speed setting should ideally persist across sessions (configurable in Settings).
*   **FR4.4 Pitch Adjustment:** Users must be able to adjust the pitch of the TTS voice.
    *   Control: Provide a slider or stepper mechanism.
    *   Range: Define a reasonable pitch range (e.g., 0.5x to 2.0x).
    *   Default: Normal pitch (1x).
    *   Persistence: Pitch setting should ideally persist across sessions (configurable in Settings).
*   **FR4.5 Voice Selection:** Users must be able to select from available TTS voices provided by the underlying native TTS engine (Expo/OS specific).
    *   Control: Provide a dropdown or list selection.
    *   Default: System default voice.
    *   Persistence: Voice selection should ideally persist across sessions (configurable in Settings).
*   **FR4.6 Universal Availability:** TTS functionality (including all controls) must be available for *all* summaries displayed in the app (newly generated or from history).

**4.5. History Management**

*   **FR5.1 History Screen:** The app must include a dedicated "History" screen.
*   **FR5.2 Summary List:** The History screen must display a list of all previously generated and saved summaries.
*   **FR5.3 List Item Display:** Each item in the history list must display at least the `Video Thumbnail` (or placeholder) and `Video Title` (or placeholder) for quick identification.
*   **FR5.4 Access Full Summary:** Tapping on a history list item must navigate the user to view the full summary card (as defined in FR3.2) for that entry.
*   **FR5.5 Deletion:**
    *   Users must be able to delete individual summaries from the history (e.g., via the "Delete Button" on the card or a swipe action in the list).
    *   A confirmation prompt should appear before deletion.
*   **FR5.6 Link in Menu:** Implement a Hamburg menu (or similar navigation pattern) that, when viewing a specific summary, provides an option/link to view/copy the original YouTube video link associated with that summary.

**4.6. Editing Summaries**

*   **FR6.1 Edit Functionality:** An "Edit" button must be present on each summary card.
*   **FR6.2 Edit Action:** Tapping the "Edit" button should allow the user to change the `Summary Type` (Brief, Detailed, Key Point) and `Summary Length` (Short, Medium, Long) for the *currently viewed video*.
*   **FR6.3 Re-generation:** Upon confirming the new Type/Length settings, the app must trigger a *new* summary generation request to the backend using the original video link and the updated parameters. The new summary will replace the previous one (or be stored as a new entry if versioning is desired - for simplicity, replacement is acceptable unless specified otherwise).

**4.7. Settings**

*   **FR7.1 Settings Screen:** The app must include a dedicated "Settings" screen.
*   **FR7.2 TTS Configuration:** The Settings screen must allow users to configure default TTS settings:
    *   Default Playback Speed
    *   Default Pitch
    *   Default Voice

**4.8. Sharing**

*   **FR8.1 Share Summary:** A "Share" button must be present on each summary card.
*   **FR8.2 Share Action:** Tapping the "Share" button must invoke the native OS sharing dialog, allowing the user to share the `Summary Text` (and potentially the original Video Link and Title) through other apps (e.g., messaging, email, social media). Format the shared content appropriately (e.g., "Summary for '[Video Title]':\n[Summary Text]\nOriginal Video: [Video Link]").

**5. Non-Functional Requirements**

*   **NFR1 Performance:**
    *   The app must be responsive and performant on all target platforms (iOS, Android, Web).
    *   UI transitions should be smooth.
    *   Summary generation time should be optimized, with clear loading/progress indicators shown to the user.
*   **NFR2 Usability:**
    *   The user interface must be clean, intuitive, and easy to navigate.
    *   Provide clear feedback to the user for actions (e.g., link validation, generation start/end, errors, cancellation).
*   **NFR3 Compatibility:**
    *   The app must function correctly on recent versions of iOS, Android, and modern web browsers.
    *   **PWA:** The web version must be a Progressive Web App, installable on the user's home screen/desktop, and offer basic offline capabilities (e.g., viewing cached history) if feasible. Configure necessary service workers and manifest files via Expo.
*   **NFR4 Reliability & Error Handling:**
    *   Implement robust error handling for all potential failure points: network requests (YouTube, Gemini API, backend), API errors, data validation, TTS engine issues, database operations, missing transcripts.
    *   Display user-friendly error messages.
    *   Handle edge cases gracefully (e.g., extremely long videos, rate limiting).
*   **NFR5 Maintainability:**
    *   Codebase must be well-documented, following standard JavaScript and React Native best practices.
    *   The project structure must be modular (as specified in Section 6.4).
    *   Code should be clean and readable.
*   **NFR6 Storage:**
    *   Summary data must be persisted reliably in the MongoDB database.

**6. Technical Specifications**

*   **TS1 Frontend:** React Native Expo (using JavaScript).
*   **TS2 Backend:** Node.js with Express.js framework.
*   **TS3 AI Integration:** Backend integrates with the **Gemini Flash-Lite** model via its official API.
*   **TS4 YouTube Data Handling:** Backend uses the `ytdlp-nodejs` library (`npm i ytdlp-nodejs`) for:
    *   Validating YouTube URLs.
    *   Fetching video metadata (Title, Thumbnail).
    *   Fetching video transcripts/captions.
*   **TS5 Database:** MongoDB for storing summary data, video metadata, and user preferences (like TTS settings if persisted server-side, though client-side persistence for settings might be simpler).
*   **TS6 Cross-Platform Build:** Utilize Expo's build services (EAS Build) or standard Expo tooling for generating iOS, Android, and Web builds.
*   **TS7 PWA Configuration:** Configure `app.json` and potentially custom service workers (if needed beyond Expo defaults) for PWA functionality (install prompt, offline caching basics).
*   **TS8 Project Structure:**
    *   Maintain a clear separation between frontend and backend code within the repository.
    *   **Root Directory:**
        *   `frontend/` (Contains all React Native Expo app code)
            *   `src/`
                *   `screens/` (Main view components: Home, History, Settings, SummaryDetail)
                *   `components/` (Reusable UI elements: SummaryCard, TextInput, Buttons, TTSControls)
                *   `services/` (API interaction logic, TTS service wrapper)
                *   `store/` or `context/` (State management, e.g., Zustand, Redux Toolkit, Context API)
                *   `navigation/` (App navigation setup)
                *   `hooks/` (Custom React hooks)
                *   `utils/` (Helper functions)
                *   `assets/` (Images, fonts)
            *   `app.json`
            *   `babel.config.js`
            *   `package.json`
        *   `backend/` (Contains all Node.js/Express.js server code)
            *   `src/`
                *   `controllers/` (Request handling logic)
                *   `routes/` (API endpoint definitions)
                *   `services/` (Business logic: Gemini interaction, ytdlp logic, DB operations)
                *   `models/` (MongoDB schema definitions - e.g., using Mongoose)
                *   `config/` (Environment variables, DB connection)
                *   `middleware/` (Error handling, validation)
                *   `utils/` (Helper functions)
            *   `server.js` or `index.js` (Main server entry point)
            *   `package.json`
        *   `.gitignore`
        *   `README.md`
    *   Ensure modules within both frontend and backend are cohesive and loosely coupled.

**7. Data Model (MongoDB)**

*   **Collection:** `summaries`
*   **Schema:**
    *   `_id`: ObjectId (Primary Key)
    *   `videoUrl`: String (Indexed, Unique potentially combined with userId/deviceId if implementing user accounts)
    *   `videoTitle`: String (Optional)
    *   `videoThumbnailUrl`: String (Optional)
    *   `summaryText`: String (Markdown format)
    *   `summaryType`: String (Enum: 'Brief', 'Detailed', 'Key Point')
    *   `summaryLength`: String (Enum: 'Short', 'Medium', 'Long')
    *   `createdAt`: Date (Timestamp)
    *   `updatedAt`: Date (Timestamp)
    *   `userId` / `deviceId`: String (Optional - consider for future user accounts or identifying unique users/devices)

**8. Final Instructions for AI Agent**

*   **Completeness:** Implement *all* requirements specified in this document. This is for a final, production-ready product, not an MVP.
*   **Quality:** Ensure the code is well-documented, follows JavaScript, React Native, and Node.js best practices, and is highly maintainable and modular as per the defined structure.
*   **Functionality:** The final application must be fully functional across iOS, Android, and Web (as an installable PWA).
*   **Testing:** Thoroughly test all features, including input methods, summary generation variations, TTS controls, history management, error handling, and cross-platform compatibility.
*   **User Experience:** Prioritize a smooth, intuitive, and user-friendly experience.
*   **Adherence:** Strictly follow the specified technical stack and libraries (React Native Expo, Node.js/Express, Gemini Flash-Lite, `ytdlp-nodejs`, MongoDB).



---
the following is the example code for the backend API endpoint to generate summaries using the Gemini 2.0 Flash-Lite model:

```javascriptconst {
  GoogleGenerativeAI,
  HarmCategory,
  HarmBlockThreshold,
} = require("@google/generative-ai");
const fs = require("node:fs");
const mime = require("mime-types");

const apiKey = process.env.GEMINI_API_KEY;
const genAI = new GoogleGenerativeAI(apiKey);

const model = genAI.getGenerativeModel({
  model: "gemini-2.0-flash-lite",
});

const generationConfig = {
  temperature: 1,
  topP: 0.95,
  topK: 40,
  maxOutputTokens: 8192,
  responseModalities: [
  ],
  responseMimeType: "text/plain",
};

async function run() {
  const chatSession = model.startChat({
    generationConfig,
    history: [
    ],
  });

  const result = await chatSession.sendMessage("INSERT_INPUT_HERE");
  // TODO: Following code needs to be updated for client-side apps.
  const candidates = result.response.candidates;
  for(let candidate_index = 0; candidate_index < candidates.length; candidate_index++) {
    for(let part_index = 0; part_index < candidates[candidate_index].content.parts.length; part_index++) {
      const part = candidates[candidate_index].content.parts[part_index];
      if(part.inlineData) {
        try {
          const filename = `output_${candidate_index}_${part_index}.${mime.extension(part.inlineData.mimeType)}`;
          fs.writeFileSync(filename, Buffer.from(part.inlineData.data, 'base64'));
          console.log(`Output written to: ${filename}`);
        } catch (err) {
          console.error(err);
        }
      }
    }
  }
  console.log(result.response.text());
}

run();
```

the following is the example code for the backend API endpoint to get the video transcript using `ytdlp-nodejs`:

```javascript
const ytdlp = require("ytdlp-nodejs");

import { YtDlp } from 'ytdlp-nodejs';

const ytdlp = new YtDlp();

const info = await ytDlp.getInfoAsync(
    'https://www.youtube.com/watch?v=dU7GwCOgvNY'
  );

console.log(info);
```