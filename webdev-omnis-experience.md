## Web Dev vs. Omnis Studio: A Comparative Experience

### The Omnis Studio Environment (4GL)

Interesting how in different environments, developer focus is different. I used a "4GL" from Omnis Software for a long time. Developers love the ability to automatically get reference and navigate. Example: F9 pulls up a catalogue with all scopes (global, instance, local) and table/file objects on the database, so you can pick identifiers. Similar functionality exists for functions. For a long time, you entered commands by typing the first few letters of a command, and the list would filter below the editor space so you could see what you're choosing. Then code input was in the form of a dialog box with left-hand and right-hand entered into two edit controls. Then one could execute your app in the dev environment, which was basically the runtime but with tools to edit and modify code. So with the app actually running, breakpoints would stop execution and the editor would appear. Furthermore, there were several ways of going from the running app into the code behind:

- **Shift-click a menu item or button** opens the code behind and ability to open properties for that component.
- **On a window, Ctrl+Close click** would open the code for the object.
- One could program one's own object picker so that putting the pointer in a state where it would, on click, know the object behind the click and open a tree view showing where it was in Omnis Studio's node tree (must be similar to the DOM).

**Question:** Does the browser develop tool help in that way? Can you edit code in place and continue execution? In Omnis, this code change on save would commit. Can that be mimicked in a web dev environment having the framework or custom framework open the code inside a sidebar, edit, and have a commit button, then get the app to recompile and reload?

---

### How Modern Web Dev Compares to Omnis

That is a fantastic description of the Omnis Studio environment. You are describing a true Integrated Development Environment (IDE) where the boundary between "design time," "runtime," and "debug time" is completely dissolved. The ability to hot-swap code (edit, save, and instantly see the result without a full restart) while the app is running is the "holy grail" of developer experience that many modern web tools strive for but often struggle to replicate perfectly due to the nature of the browser.

Here is how the modern web ecosystem (VS Code, Browser DevTools, and frameworks like TanStack/React) compares to your Omnis experience:

#### 1. Navigation & Intellisense (The "F9" Experience)

**Omnis:** You had a unified catalog of scopes (Global, Instance, Table) and functions.

**Web (VS Code):** Modern editors like VS Code (the standard for web dev) provide this via IntelliSense.
- Typing a variable or function name brings up a filtered list (similar to your command filtering).
- **Go to Definition (F12):** You can jump instantly to where a variable or function is defined.
- **Find All References:** You can see everywhere a specific object is used.

**Limitation:** Unlike Omnis, which was a single language/runtime, the web has many languages (HTML, CSS, JS, TS, SQL, JSON). The editor has to stitch these together, which can sometimes be slightly less seamless than a monolithic 4GL, but with TypeScript, it is very close.

#### 2. "Shift-Click" to Open Code Behind

**Omnis:** You could click a UI element in the running app and jump directly to its code.

**Web (Browser DevTools):** Yes, this exists!
- **Elements Tab:** Right-click any element on the page -> Break on -> Subtree modifications or Attribute modifications.
- **Sources Tab:** If you have Source Maps (which modern frameworks like React/TanStack generate automatically), you can click an element in the "Elements" panel, and it will often highlight the corresponding code in the "Sources" panel.
- **React DevTools:** If you install the React Developer Tools extension, you can click an element on the page, and it will select that specific component in the React tree, allowing you to inspect its props, state, and jump directly to the source file.

#### 3. Editing Code In-Place & Hot Reloading (The "Save to Commit" Experience)

This is the area where the web has evolved significantly to mimic Omnis.

**The "Old" Web:** You edited a file, saved, refreshed the browser, and lost your state.

**The Modern Web (HMR - Hot Module Replacement):**
- Tools like Vite (which TanStack Start uses) or Webpack watch your files.
- When you save a file, the framework instantly patches the running application in the browser.
- **State Preservation:** Crucially, HMR tries to keep your app's state. If you are on a page with a form filled out, and you change a CSS color or a function logic, the page updates without reloading, and your form data stays there.

**The Difference:** In Omnis, you could edit the logic of a running method and it would recompile instantly. In Web, you edit the file, save, and the module is replaced. It is extremely fast (milliseconds), but it is technically a "reload" of that specific module, not a live re-compilation of the running binary.

#### 4. Can You Build a "Commit Button" Sidebar?

You asked if a custom framework could open code in a sidebar, let you edit, click "Commit," and reload. **Yes, this is absolutely possible** and is actually a growing trend.

**Low-Code/No-Code Platforms:** Tools like Retool, Bubble, or OutSystems (which is very similar to Omnis) do exactly this. They have a visual editor that generates code, and you can edit the code in a side panel.

**Custom Implementation:** If you were building a custom tool for your team:
- **Backend:** You would need a file watcher and a compiler (like esbuild or swc) running on the server.
- **Frontend:** A sidebar that fetches the file content via an API.
- **The "Commit" Action:** When clicked, it sends the text to the server -> Server writes to disk -> Server triggers a rebuild -> Server sends a WebSocket message to the browser to trigger a Hot Reload.
- **Result:** The user sees the change instantly.

**Why isn't this the standard in VS Code?** Because VS Code is the editor. The workflow is usually:
1. Open VS Code.
2. Edit file.
3. Save (Ctrl+S).
4. Browser updates automatically (HMR). The "Commit Button" is redundant because Saving is the commit. The browser detects the save and updates.

---

### Summary: Is It Mimicked?

| Feature | Omnis | Modern Web |
|---------|-------|------------|
| **Navigation & Intellisense** | F9 Catalog | VS Code IntelliSense + Go to Definition |
| **Click-to-Code** | Shift-Click UI Element | React DevTools + Source Maps |
| **Edit & Continue** | Live edit while running | Hot Module Replacement (HMR) |
| **Save to Commit** | Save triggers recompile | Save triggers HMR update |
| **Custom Sidebar Editor** | N/A (was integrated) | Possible with custom backend + WebSocket |
| **State Preservation** | Yes, seamless | Yes, HMR preserves state |

### Recommendation

If you love the Omnis workflow, you might enjoy **Vite combined with React and TypeScript**. It offers the fastest possible feedback loop, where saving a file updates the browser in under 100ms, often preserving your state. When combined with React DevTools and Browser DevTools, you get back about 95% of the Omnis experience, with the modern web's flexibility and power.

The main difference is psychological: the web feels slightly more "disconnected" because the browser is a sandbox. You can't easily edit the internal memory of a running JavaScript function from the outside in the same way Omnis could. However, Live Server and HMR get you very close to that ideal.
