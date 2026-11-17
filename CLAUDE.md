# carolsingalongs.org

Static directory of carol sing-along events in Windsor, Ontario. Hosted on GitHub Pages (`CNAME` = carolsingalongs.org). Run by Steve Grubich. No build step: plain HTML/CSS/JS, one file per year.

## Files
- `index.html` is the **current year** page (2026). Header, 3 FAQ dropdowns, welcome box, event cards, Buddy quote dividers, About This Guide, footer.
- `2025.html` is the **archive** of last year. Has a banner at the top linking back to `index.html`. Treat as frozen; only fix real errors.
- `images/<year>/` holds flyers (`images/2025/`, `images/2026/`). Reference them with relative paths, e.g. `images/2026/Name.jpg`. Never embed base64 images.
- `og-image.jpg` (social preview) stays in the root.
- `carol-singalong-windsor-2025.html` is an obsolete early draft. Do not edit or link to it.
- Every page's CSS is inline in its own `<head>`. There is no shared stylesheet, so a style change must be made in each page that needs it.

## How we work (important)
- **Never push to `main`.** Make a branch, commit, push, and open a pull request. Steve reviews and merges. Opening a PR with `gh pr create` fails here (GraphQL blocked); use `gh api repos/HospitaleroAdvisors/carolsingalongs/pulls -f title=... -f head=BRANCH -f base=main -F body=@file`.
- **Batch events**: when Steve gives several events at once, put them in one PR. One event = one PR is fine when urgent.
- Steve supplies event text and flyer images in chat. Save each flyer to `images/<year>/` with a descriptive filename (e.g. `Church_Name_Event_Dec_14.jpg`), and use the first line of the PR body to list the events added.
- Event outreach to hosts is handled separately in Claude Chat; don't draft campaigns here unless asked.
- After editing, open the page in headless Chromium (Playwright is installed) at desktop (1200px) and phone (390px) widths: confirm no console errors, no broken images, and that every dropdown opens.
- Don't invent event details. If a time, address or link is missing, ask or use "Date TBA".

## Event cards
Put cards in **date order**, in the area where the 2025 cards were (between the welcome box/FAQs and "About This Guide"). Pick the layout that fits the flyer; copy from `2025.html` for exact markup.

1. **Portrait flyer (side by side)**: `<div class="event-card riverside-event">` with `.event-content` (title, date, location, optional `.event-description`, optional `.social-media-link`) and `.event-flyer` (flyer in `<a target="_blank">`).
2. **Landscape flyer**: `<div class="event-card">` with `.event-title-outside` and a `.event-table` (`.text-column` + `.flyer-column`).
3. **No flyer**: `<div class="event-card">` with `.event-title`, `.event-date-time`, `.event-location`, optional description and link.

Conventions:
- Title: `Event Name @ Venue`.
- Date line: `📅 Sun, Dec 7, 2026 • 5:30 PM - 7:30 PM`. Location line: `📍 Street address, Windsor, ON`.
- Link button text: "Event details on Facebook" or "Event details on website". Omit if there's no link.
- Alt text on flyers describes the event.
- Decorative dividers (Buddy/Jovie quote, participation note, a repeat of the Lessons & Carols dropdown) can be placed between cards to break up a long list, as in `2025.html`.

## Keep as-is
- The design (colors, fonts, rounded cards), the Buddy Hobbs quotes, the three FAQ dropdowns, the "About This Guide" box, and the footer with carolsingalong@gmail.com.
- The accordion script at the bottom of each page (event delegation, sizes panels with `scrollHeight`) and the CSS that hides closed panel borders. Don't go back to inline `onclick`.

## When the first 2026 event is added
Replace the welcome box text ("2026 listings are on the way") with a short "more events are being added as hosts confirm" line, and keep the "Browse the 2025 Directory" button and organizer email. Make this change in the same PR as the first event card, and mention it in the PR description. No need to ask first.

## Rolling over to a new year (each autumn)
1. Copy the finished `index.html` to `<year>.html` and add the "return to current year" banner (copy it from `2025.html`). Update its title and og:url.
2. Move that year's flyers to `images/<year>/` and fix the `<img>` paths.
3. Reset `index.html` to the new year: new title/h1/meta, remove event cards, restore the welcome box, point its archive button at the previous year's page, and add an empty `images/<newyear>/.gitkeep`.

## Contact
Event organizers submit to carolsingalong@gmail.com.
