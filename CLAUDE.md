# carolsingalongs.org

Static directory of carol sing-along events in Windsor, Ontario. Hosted on GitHub Pages (`CNAME` = carolsingalongs.org). Run by Steve Grubich. No build step: plain HTML/CSS/JS, one file per year.

## Files
- `index.html` is the **current year** page (2026). Header, FAQ dropdowns interleaved with event cards, a welcome box, About This Guide, footer. Current order: header, "What is a carol sing-along?" dropdown, event cards (date order) with the welcome box and "What do you get out of a sing-along?" dropdown placed between them, About This Guide, footer. As more events are added, keep the dropdowns and welcome box spread between cards rather than bunched together.
- `2025.html` is the **archive** of last year. Has a banner at the top linking back to `index.html`. Treat as frozen; only fix real errors.
- `images/<year>/` holds flyers (`images/2025/`, `images/2026/`). Reference them with relative paths, e.g. `images/2026/Name.jpg`. Never embed base64 images.
- `og-image.jpg` (social preview) stays in the root.
- Every page's CSS is inline in its own `<head>`. There is no shared stylesheet, so a style change must be made in each page that needs it.

## How we work (important)
- **Never push to `main`.** Make a branch, commit, push, and open a pull request. Steve reviews and merges. Opening a PR with `gh pr create` fails here (GraphQL blocked); use `gh api repos/HospitaleroAdvisors/carolsingalongs/pulls -f title=... -f head=BRANCH -f base=main -F body=@file`.
- **Batch events**: when Steve gives several events at once, put them in one PR. One event = one PR is fine when urgent.
- Steve supplies event text and flyer images in chat. Save each flyer to `images/<year>/` with a descriptive filename (e.g. `Church_Name_Event_Dec_14.jpg`), and use the first line of the PR body to list the events added.
- Event outreach to hosts is handled separately in Claude Chat; don't draft campaigns here unless asked.
- After editing, open the page in headless Chromium (Playwright is installed) at desktop (1200px) and phone (390px) widths: confirm no console errors, no broken images, and that every dropdown opens.
- Don't invent event details. If a time, address or link is missing, ask or use "Date TBA".

## Event cards
Put cards in **date order**, between the header and "About This Guide", with the dropdowns and welcome box interspersed (see Files). Pick the layout that fits the flyer; copy from `2025.html` for exact markup.

1. **Portrait flyer (side by side)**: `<div class="event-card riverside-event">` with `.event-content` (title, date, location, optional `.event-description`, optional `.social-media-link`) and `.event-flyer` (flyer in `<a target="_blank">`).
2. **Landscape flyer**: `<div class="event-card">` with `.event-title-outside` and a `.event-table` (`.text-column` + `.flyer-column`).
3. **No flyer**: `<div class="event-card">` with `.event-title`, `.event-date-time`, `.event-location`, optional description and link.

Conventions:
- Title: `Event Name @ Venue`.
- Date line: `📅 Sun, Dec 7, 2026 • 5:30 PM - 7:30 PM`. Location line: `📍 Street address, Windsor, ON`.
- Link button text: "Event details on Facebook" or "Event details on website". Omit if there's no link.
- Alt text on flyers describes the event.
- Decorative dividers (Buddy/Jovie quote, participation note) were left out of 2026 while there were only two listings. Bring them back between cards as the list grows, as in `2025.html`.
- **Flyer pending:** if a host has confirmed but the flyer isn't ready, use the table layout with `<div class="flyer-pending">Flyer Pending</div>` in place of the flyer link/image. When the flyer arrives, swap in the `<a><img></a>` and delete the placeholder.
- Mention audience singing in the description only when Steve confirms it.

## Keep as-is
- The design (colors, fonts, rounded cards), the Buddy Hobbs header quote, the FAQ dropdowns, the "About This Guide" box, and the footer with carolsingalong@gmail.com.
- The "Lessons & Carols Service: What is it?" dropdown was removed from 2026 for now. Add it back (copy from `2025.html`) directly above the first Lessons & Carols event when one is listed.
- The accordion script at the bottom of each page (event delegation, sizes panels with `scrollHeight`) and the CSS that hides closed panel borders. Don't go back to inline `onclick`.

## When the first 2026 event is added
Done: the welcome box now has no heading and reads "More December 2026 carol sing-alongs are being added...", with the "Browse the 2025 Directory" button and organizer email. Steve kept the "December" framing even though the first event is Nov 29. Propose any further wording changes in chat first and wait for his approval.

## Rolling over to a new year (each autumn)
1. Copy the finished `index.html` to `<year>.html` and add the "return to current year" banner (copy it from `2025.html`). Update its title and og:url.
2. Move that year's flyers to `images/<year>/` and fix the `<img>` paths.
3. Reset `index.html` to the new year: new title/h1/meta, remove event cards, restore the welcome box, point its archive button at the previous year's page, and add an empty `images/<newyear>/.gitkeep`.

## Contact
Event organizers submit to carolsingalong@gmail.com.
