# Mobile responsiveness update

Use the complete project folder so the new `responsive.css` file is included.
Run the project as before: `npm run dev` (requires Node.js 22 or newer).

Changes:
- Compact phone header with larger search, shortlist and menu controls.
- Expandable product categories in mobile navigation, Escape support, keyboard focus handling and background scroll lock.
- Single-column phone hero and solution layouts; corrected wide tile grid spans.
- Two-column product cards on most phones, one column on very narrow phones.
- Shorter swipeable category cards, clearer filters, sorting and pagination.
- Phone-sized product images, readable specifications and full-width action buttons.
- Visible search close button and scrollable search, testimonial and shortlist panels.
- Larger form inputs to prevent automatic input zoom on iPhone.
- Improved footer, service steps, maps, partner cards and admin editor layouts.
- Responsive styles are served by the Node server as well as static hosting.

Validation: client and server JavaScript syntax checks passed; the existing integration suite passed, including a new check for the responsive stylesheet endpoint. Visual browser/device testing was unavailable in the editing environment. Please check the home page, catalog, product page, menu, search and shortlist on your phone before publishing.

Desktop styling remains in index.html; responsive changes are in responsive.css.

## Home page refinements

On screens up to 700px:
- Explore our solutions becomes a horizontal, swipeable category carousel that advances every four seconds while visible. It pauses during dragging, keyboard interaction, when the page is hidden, and for reduced-motion preferences. Pause/play and previous/next controls are included.
- Tap–Verify–Enter uses a short mobile summary, three compact process steps and a smaller animation contained within its card. The longer desktop copy, bullet list and repeated CTA are hidden on mobile.
- The homepage statistics remain in a two-by-two grid on narrow phones.

These additions do not alter desktop layouts. Client JavaScript syntax checks and server integration tests passed. Actual phone/browser visual testing remains outstanding.
