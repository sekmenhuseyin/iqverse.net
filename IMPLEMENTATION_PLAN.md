## Phased migration plan

A careful migration plan is now prepared and saved in the session plan file. It is organized into phases so you can review and approve each stage before work continues.

### Plan summary
- Preserve the current URL structure, including the homepage and tool subpaths such as /json/, /qrforge/, /regex/, and the other existing tool routes.
- Move the site to a Next.js App Router structure while keeping the output fully static.
- Rebuild the experience using shared layouts and reusable components, but keep tool logic client-side so the app remains privacy-first.
- Split the work into reviewable phases so each milestone can be approved before the next one begins.

### Proposed phases
1. Discovery and route baseline
2. Next.js foundation and static routing
3. Shared layout and homepage architecture
4. First batch of tool page migrations
5. Remaining tool page migrations
6. SEO, export hardening, and deployment

### What each phase will deliver
- A clear route map and migration scope
- A working static Next.js app with the same public paths
- Reusable layout and component structure
- Tool pages migrated one batch at a time
- A production-ready static export and deployment path

### Recommended implementation approach
- Use the current site as the source of truth for content, layout, and tool behavior.
- Keep explicit route folders for important tools so the URLs stay stable.
- Reuse shared components for header, hero sections, cards, buttons, and tool shells.
- Avoid server-side dependencies so the exported site remains fully static.

### Suggested review checkpoints
- After route mapping and scope confirmation
- After the first working static Next.js build
- After the shared layout and homepage structure are in place
- After the first batch of tools is migrated
- After all tool routes are implemented
- After the final static export and deployment verification

If you want, I can now refine this into a more detailed implementation checklist for Phase 1 only, so you can approve the first milestone before any code changes begin.
