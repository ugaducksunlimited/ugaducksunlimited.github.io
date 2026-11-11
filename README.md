# Ducks Unlimited at UGA: Website

The whole chapter website is **one file: `index.html`**. All six pages (Home, About, Exec Board, Events, Sponsors, Join), the styling, the logos and the code are inside it. There's nothing to install or build.

You can update it two ways:

- **With an AI tool** like Claude or ChatGPT. This is the easiest way, and you don't need to know any code.
- **By hand** in a text editor or right on GitHub.

Either way, the routine is the same: **make one change → preview it → commit it.**

---

## Option 1: Update the site with AI (recommended)

### Steps

1. **Download `index.html`** from this repo. Open the file, click the download icon (or **Raw**, then save the page).
2. **Open Claude or ChatGPT** and start a new chat.
3. **Upload the file.** Attach it with the paperclip or **+** button. The file is too large to paste in as text.
4. **Describe the change** using the prompt below.
5. **Make the change** the AI gives you (see "Two ways to get changes back" below).
6. **Preview:** double-click `index.html` to open it in your browser and click through every page.
7. **Upload it back to GitHub:** in the repo, click **Add file → Upload files**, drop in the new `index.html` and click **Commit changes** with a short note like "Updated officer names."

### Prompt to copy

> I've attached `index.html`, a single-file website for our Ducks Unlimited chapter. I want to make this change: **[describe it]**.
>
> Please give me the exact text to search for in the file and the exact text to replace it with, as before-and-after code blocks. Don't rewrite the whole file. Don't change anything else, and leave the long `data:image/...` image codes alone.

### Two ways to get changes back

- **Before-and-after snippets (safest).** The prompt above asks for these. Open `index.html` in a text editor (VS Code is free) or edit it on GitHub with the pencil icon. Use **Ctrl+F** (**Cmd+F** on Mac) to find the "before" text, paste in the "after" text, then save.
- **A whole new file.** Some tools, like Claude with file creation turned on, can hand back a finished `index.html` to download. That's fine, but check it before uploading:
  - The new file should be about the same size as the old one (roughly 140 KB).
  - Every page and logo should still show up in your browser.

  If the logos are missing or the file is much smaller, the AI cut something out. Don't use that file.

### Example requests

- "Change the contact email everywhere it appears to **duclub@uga.edu**."
- "Add a new officer card for **Jane Doe, Treasurer, Junior, Finance**, with the quote: '...'."
- "Add an event to the calendar on **February 21** labeled **Banquet**, using the fundraiser color."
- "Replace the 'Add photo' placeholder on **Harvey Roddenberry's** card with the image `images/harvey.jpg`."
- "Change the announcement bar so the third message says **Banquet tickets on sale now** and links to the Events page."
- "Move the calendar to the **2027–2028** school year."

### Tips for working with AI

- **One change per chat works best.** Big multi-part requests are where mistakes happen.
- **Always preview before committing.** AI tools can be confidently wrong.
- **Never paste passwords** or private member information into an AI chat.
- If something breaks, ask: "Here's my file. After my last change, the **[calendar / menu / a page]** stopped working. What went wrong?"

---

## Option 2: Update the site by hand

### Ground rules

- **Only change the words between tags.** In `<p>Hello there</p>`, change `Hello there` and leave `<p>` and `</p>` alone.
- **Write `&amp;` instead of `&`** in text, for example `Events &amp; Outreach`.
- **Be careful in the code at the bottom** (after `<script>`). One missing comma or quote mark can break the calendar or the announcement bar.
- **Don't touch the long image codes** that start with `data:image/webp;base64,...` unless you're replacing that image.

### Editing

- **On GitHub:** open `index.html`, click the pencil icon, make the change, then click **Commit changes**.
- **On your computer:** open the file in a text editor, save, preview it in your browser, then upload it to GitHub.

Use **Ctrl+F** / **Cmd+F** to find what you want to change. Search terms are listed below.

---

## Where everything is

| To change… | Search for |
|---|---|
| Colors | `:root{` |
| Menu buttons | `<nav class="primary"` |
| Announcement bar messages | `var items = [` |
| Home page | `========== HOME` |
| FAQ | `Frequently asked questions` |
| About page | `========== ABOUT` |
| Contact info | `Contact us` |
| Join page (Instagram/Facebook) | `========== JOIN` |
| Officer cards | `Meet the exec board` |
| Calendar events | `function getMonthEvents` |
| School year on the calendar | `var schoolYear = [` |
| Sponsor logos | `sponsor-grid` |
| Footer | `<footer class="site">` |

---

## Common edits by hand

### Contact email and meeting location

- **Email** appears in several places, including the Contact section and the "Email us" button on the Sponsors page. Search for `ducksunlimited@uga.edu` and replace **every** match.
- **Meeting location:** search for `Where we meet`.
- Once the real info is in, delete the two reminder lines: `(Update with your chapter's real address.)` and `(Confirm your chapter's actual meeting location.)`.

### Instagram and Facebook links

Search for `instagram.com` or `facebook.com`. Change both the link (`href="..."`) and the text people see.

### Officer cards

Each officer is one block like this:

```html
<div class="exec-card">
  <div class="exec-photo"> ... </div>
  <h3>Harvey Roddenberry</h3>
  <div class="exec-role">Chairman / President</div>
  <dl class="exec-fields">
    <div class="field-row"><dt>Year</dt><dd>Junior</dd></div>
    <div class="field-row"><dt>Major</dt><dd>Agribusiness</dd></div>
  </dl>
  <blockquote class="exec-quote">&ldquo;Quote goes here.&rdquo;</blockquote>
</div>
```

- **Edit an officer:** change the name, role, year, major or quote text.
- **Add an officer:** copy one whole block, from `<div class="exec-card">` to its matching `</div>`, and paste it after another card.
- **Remove an officer:** delete their whole block.
- **Add a headshot:** inside `<div class="exec-photo">`, replace the camera icon (`<svg>...</svg>`) and `<span>Add photo</span>` with:
  `<img src="images/harvey.jpg" alt="Harvey Roddenberry">`

### Sponsors

Search for `sponsor-grid`. Each sponsor is one tile, and the tier sets its size:

| Tier | Class | Size |
|---|---|---|
| Platinum | `tier-platinum` | Largest |
| Gold | `tier-gold` | Medium |
| Community | `tier-silver` | Small |

To add a real logo, replace everything **inside** a tile with:
`<img src="images/sponsor-name.png" alt="Sponsor Name">`

Once real logos are in, delete the note that starts with `Logo tiles above are placeholders`.

### Announcement bar

Search for `var items = [`. Each line is one message:

```js
{ text: "New members always welcome", page: "join" },
```

- `text` is what shows in the bar. `page` is where clicking it goes: `home`, `about`, `execboard`, `events`, `sponsors` or `join`.
- Every line except the last ends with a comma.
- **If you add or remove a message**, add or remove a matching `<span class="ticker-dot"></span>` (search `id="tickerDots"`).
- **If you change the first message**, change the text at `id="tickerText"` to match.

### Calendar

Search for `function getMonthEvents`.

- **Meetings** are set to the 2nd and 4th Thursday of each month.
- **To add an event on a set date**, paste this just above `return events;` (example: November 14):

```js
if(month === 10){ // November
  events.push({ day: 14, label: "Social", color: "var(--water)" });
}
```

**Months start at 0:** Jan = 0, Feb = 1, Mar = 2, Apr = 3, May = 4, Aug = 7, Sep = 8, Oct = 9, Nov = 10, Dec = 11

**Colors:** `var(--mallard)` = meeting, `var(--rust)` = volunteer workday, `var(--water)` = fundraiser or chapter event

Keep labels to one or two words, since they need to fit in a small box. Only one event shows per day.

**New school year:** search for `var schoolYear = [` and add 1 to every year (2026 → 2027, 2027 → 2028).

### Images

The logos are built into the file as long `data:image/...` codes, which is why the file is large. To replace one:

1. Upload the new image to the repo, ideally into an `images/` folder. Keep it under about 300 KB.
2. Find the `<img src="data:image/...` you want to replace. The UGA badge logo appears three times: header, home page and footer.
3. Replace everything between the quotes after `src=` with the file path, like `src="images/logo.png"`.

### Colors

Search for `:root{`. Each color is defined once and used across the whole site.

| Name | Used for |
|---|---|
| `--mallard` | Green buttons and accents |
| `--rust` | Red accents |
| `--water` | Brown accents |
| `--bg` / `--bg-alt` | Page backgrounds |
| `--ink` / `--ink-soft` | Text |

The first `:root{` block is light mode. The **two** blocks right after it are dark mode, so change a dark mode color in both.

---

## Still needs real info

- [ ] Contact email
- [ ] Meeting location
- [ ] Officer headshots
- [ ] Sponsor logos
- [ ] Real event dates on the calendar

---

## If something breaks

- **A page is blank or the calendar disappeared:** a comma, quote or bracket was probably deleted in the `<script>` section at the bottom.
- **The layout looks off:** a tag like `<div>` probably lost its closing `</div>`.
- **Undo a change on GitHub:** open `index.html`, click **History**, open the last version that worked, copy it and paste it back in.
- **Ask an AI:** upload the broken file and describe what stopped working.
