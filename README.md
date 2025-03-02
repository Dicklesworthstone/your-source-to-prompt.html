# Your Source to Prompt (Securely, On Your OWN Machine!)


Wait, ANOTHER tool to take code files and turn them into a single prompt file for Large Language Models? How many tools like this does the world need?! There are already so many:

1. [files-to-prompt](https://github.com/simonw/files-to-prompt)
2. [repo2txt](https://repo2txt.simplebasedomain.com/)
3. [code2prompt](https://github.com/mufeedvh/code2prompt)
4. [repomix](https://github.com/yamadashy/repomix)
5. [ingest](https://github.com/sammcj/ingest)
6. [1filellm](https://github.com/jimmc414/1filellm)
7. [repo2file](https://github.com/artkulak/repo2file)
8. [code-to-gpt](https://github.com/skelouse/code-to-gpt)

… and others keep cropping up. Yet, **Your Source to Prompt** stands out with a unique set of capabilities that address many pain points these existing tools don’t fully resolve.

In fact, I made it for myself to scratch my own itch, because I was wasting so much time using other tools that caused me to repeat myself over and over, or which made it difficult to work with private repos.

## Screenshots of it in Action (Click to see larger versions):
|                               |                               |
|-------------------------------|-------------------------------|
| *Choose files visually:* ![Screenshot 1](https://raw.githubusercontent.com/Dicklesworthstone/your-source-to-prompt.html/refs/heads/main/screenshots/screenshot_1.png) | *String filters and quick select options:* ![Screenshot 2](https://raw.githubusercontent.com/Dicklesworthstone/your-source-to-prompt.html/refs/heads/main/screenshots/screenshot_2.png) |
| *Add preamble text and goals; save and load presets:* ![Screenshot 3](https://raw.githubusercontent.com/Dicklesworthstone/your-source-to-prompt.html/refs/heads/main/screenshots/screenshot_3.png) | *Easily save the final output text as a file or copy to clipboard:* ![Screenshot 4](https://raw.githubusercontent.com/Dicklesworthstone/your-source-to-prompt.html/refs/heads/main/screenshots/screenshot_4.png) |

---

## Overview

**Your Source to Prompt** is a single `.html` file that, when opened in a modern browser (like Chrome), provides a complete GUI to easily select code files and combine them into a single text output. The key innovation is that it runs entirely in your browser, with no external dependencies or services. It’s:

- **Local and Secure**: Your code never leaves your machine.
- **No Installation Hassles**: No Python, no Node.js, no CLI fiddling. Just a single, self-contained HTML file that you open in any modern browser and then it "just works."
- **Works with Any Folder**: Not limited to Git repos.
- **Optimized for Repeated Use**: Save and load presets of file selections and settings.

This tool is all about letting you focus on your actual LLM-driven coding tasks without wrestling with complex pipelines or risking your code’s privacy.

---

## Key Advantages

1. **Fully Local & Secure**: Just open the `.html` file. The modern File System Access API lets you read from your local drive directly. No server, no GitHub auth tokens, no privacy concerns.

2. **No Dependencies**: Requires only a recent Chromium-based browser. No installations, no package managers.

3. **Use with Any Folder or Repo**: Perfect for private codebases or just a random set of files you want to show the LLM.

4. **Presets to Save Time**: Preset functionality lets you store your favorite file selections and reload them instantly. Save to `localStorage` or export/import as JSON.

5. **Efficient File Selection**:
   - String-based filtering to quickly find files.
   - Convenient mass selection (e.g., “Select all React files”).
   - Toggle all text files with one click.
   
6. **Context Size Awareness**: A tally of total size and lines is always visible, with warnings if you’re likely to exceed context windows (like GPT-4 or Claude limits).

7. **Hierarchical Structure Preview**: Automatically includes a tree-like structure showing file sizes and line counts before the code listings, providing vital context to the LLM.

8. **Minification to Save Space**: Optionally minify JS, CSS, HTML, JSON, and even trim other text files for maximum context efficiency.

9. **Custom Preamble & Goal**: Prepend your combined output with a preamble and a stated goal so the LLM understands the context and your intentions before reading the code.

10. **Export/Import Presets**: Share or backup your presets easily so you don't need to waste time selecting the same complex grouping of files over and over again!

11. **User Friendly UI with Dark Mode**: It looks nice and is easy to get started, with comprehensive tooltips explaining what everything does.

---

## How It Works Under the Hood

### Browser File System Access API

- On clicking "Select Folder," the tool uses the File System Access API to prompt you for a local directory.
- Once granted, it reads the contents of that directory (and subdirectories), filtering out ignored files (via `.gitignore` or default patterns).
- Everything happens locally, in-browser.

### Building the File Tree

- The tool scans your chosen folder, recursively enumerating files and directories.
- `.gitignore` patterns are applied to skip irrelevant files.
- Files are displayed in a nested tree structure.
- Text files (based on known extensions) get checkboxes, so you can select which ones to include in the final prompt.

### Preset Management

- Selections and configurations are stored in `localStorage` as JSON.
- Name and save a preset to quickly restore a known configuration.
- Export and import presets to/from a `.json` file for portability.

### Context Warnings

- The UI calculates total selected size and line count as you select files.
- Approximate warnings appear if you exceed thresholds likely to cause trouble with certain LLM contexts.

### Preamble & Goal

- Preamble: A custom introduction or explanation.
- Goal: A concise statement of what you want to achieve.
- These help frame the LLM prompt so that the code is contextualized and not just dropped in cold.

### Minification Steps

- Uses client-side libraries:
  - **Terser** for JS/TS minification.
  - **csso** for CSS.
  - **html-minifier-terser** for HTML.
  - JSON is re-serialized to a single line.
  - Other text files have trailing whitespace trimmed.
  
This process helps fit larger codebases into the LLM’s context window, and it tells you the space savings so you can decide if it's worth it.

---

## How to Use the Tool Step-by-Step

1. **Get the HTML File**: Download `your-source-to-prompt.html` from this repository to your computer.

2. **Open it in Chrome**:  
   Just double-click or drag it into your browser.

3. **Select a Folder**:  
   Click "Select Folder," choose your code directory. The tool will load and display your files.

4. **Filter and Select Files**:  
   Use the search bar to quickly find files by name. Use the quick-select buttons to grab all files of a certain type. Toggle all text files if that’s easier.

5. **Set Up Preamble and Goal (Optional)**:  
   If desired, enable preamble and goal options and enter your custom text.

6. **Minify Output (Optional)**:  
   Check the minify box to reduce file size. This can help when dealing with large projects.

7. **Check the Tally**:  
   The total selected size and line count appear in the top-right corner. Heed the warnings if any appear.

8. **Save a Preset (Optional)**:  
   If you want to reuse these selections and settings, enter a name and click "Save Preset." You can load it next time without re-selecting everything.

9. **Combine Files**:  
   Click "Combine Selected Files." The tool generates a single text output containing:
   - Your preamble (if any)
   - Your goal (if any)
   - A hierarchical summary of selected files
   - Each file preceded by a header line with the filename

10. **Copy or Download the Result**:  
    Use the provided buttons to copy the combined text to your clipboard or download it as a `.txt` file. Paste it into your LLM prompt and start working!

---

## Example Workflow

**Scenario**: You want your LLM to help refactor a Node.js API.

1. Open `your-source-to-prompt.html` in Chrome.
2. Select your project folder.
3. Filter by "api" to find backend files quickly.
4. Use file type filters to select all `.js` files.
5. Enable the preamble: "Below are the main API files from my Node.js project..."
6. Add a goal: "Goal: Refactor the API handlers to follow better error-handling patterns."
7. Enable Minify Output to save space.
8. Combine the files.
9. Copy the output and paste into the LLM’s prompt.

Now the LLM sees a well-structured, minimized project context along with your stated goal, all fully local and secure.

---

## Technical Details & Maintenance

- Written in pure HTML/JS with TailwindCSS for styling and Tippy.js for tooltips.
- Uses browser-based libraries from CDNs for minification and UI enhancements.
- Data never leaves your machine.
- Works best in Chromium-based browsers supporting the File System Access API.
- Presets stored in `localStorage`; easily exported/imported as JSON.

---

## Browser Compatibility

For best results, use a Chromium-based browser like Chrome. This ensures full support for the File System Access API. Other browsers (Firefox, Safari) may not support the directory access features yet.

---

## Conclusion

**Your Source to Prompt** may be one of many such tools, but it offers a unique combination of local operation, no-install convenience, powerful preset management, efficient file selection, minification, and thoughtful UI enhancements. It lets you quickly and securely create a well-structured prompt context for your LLM, making your AI-driven coding sessions more streamlined and effective.

License: MIT License Applies 


---

Thanks for your interest in my open-source project! I hope you find it useful. You might also find my commercial web apps useful, and I would really appreciate it if you checked them out:

**[YoutubeTranscriptOptimizer.com](https://youtubetranscriptoptimizer.com)** makes it really quick and easy to paste in a YouTube video URL and have it automatically generate not just a really accurate direct transcription, but also a super polished and beautifully formatted written document that can be used independently of the video.

The document basically sticks to the same material as discussed in the video, but it sounds much more like a real piece of writing and not just a transcript. It also lets you optionally generate quizzes based on the contents of the document, which can be either multiple choice or short-answer quizzes, and the multiple choice quizzes get turned into interactive HTML files that can be hosted and easily shared, where you can actually take the quiz and it will grade your answers and score the quiz for you.

**[FixMyDocuments.com](https://fixmydocuments.com/)** lets you submit any kind of document— PDFs (including scanned PDFs that require OCR), MS Word and Powerpoint files, images, audio files (mp3, m4a, etc.) —and turn them into highly optimized versions in nice markdown formatting, from which HTML and PDF versions are automatically generated. Once converted, you can also edit them directly in the site using the built-in markdown editor, where it saves a running revision history and regenerates the PDF/HTML versions.

In addition to just getting the optimized version of the document, you can also generate many other kinds of "derived documents" from the original: interactive multiple-choice quizzes that you can actually take and get graded on; slick looking presentation slides as PDF or HTML (using LaTeX and Reveal.js), an in-depth summary, a concept mind map (using Mermaid diagrams) and outline, custom lesson plans where you can select your target audience, a readability analysis and grade-level versions of your original document (good for simplifying concepts for students), Anki Flashcards that you can import directly into the Anki app or use on the site in a nice interface, and more.
