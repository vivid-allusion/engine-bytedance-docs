# BytePlus docs — capture 2026-11-07

Full English documentation from <https://docs.byteplus.com/en/docs>, saved as markdown.

- **22,972 pages** across **110 products** (20.3 million words, 197 MB of text).
- The site serves every page as markdown at
  `https://docs.byteplus.com/docs/en/<product>/<document-code>.md`; each file here is that
  response verbatim, with a small YAML header added (title, product, source URL, last updated).
- One folder per product, with subfolders mirroring the site navigation, plus a `README.md`
  index per product and one at the root. `manifest.json` lists every page with its source URL
  and byte size.
- Two pages are empty on BytePlus's side (`aidap/.../DescribeSupabaseDeployEnvVars` and the
  Flutter player download page under `byteplus-vod`) and are marked as such.
- Internal links and images are absolute URLs pointing at the live site, so they resolve while
  online; no images were downloaded.

The page list came from the site's own navigation API
(`https://www.byteplus.com/api/doc/getDocList?LibraryCode=<product>&type=online&DataSchema=all_second_nav`),
filtered to published content pages, so drafts, folders, and test libraries are excluded.
