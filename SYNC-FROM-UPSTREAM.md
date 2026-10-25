# Refresh from upstream

Run from the repo root when you want the latest kit from GitHub (without re-cloning the whole blog):

```bash
tmpdir=$(mktemp -d)
git clone --depth 1 --filter=blob:none --sparse https://github.com/woosal1337/blog.git "$tmpdir/blog"
cd "$tmpdir/blog"
git sparse-checkout set videos/ep01-the-cure-for-ai-slop
cd -
rsync -a --delete "$tmpdir/blog/videos/ep01-the-cure-for-ai-slop/asd-ste100/" ./asd-ste100/
rsync -a --delete "$tmpdir/blog/videos/ep01-the-cure-for-ai-slop/experiment/" ./experiment/
cp "$tmpdir/blog/videos/ep01-the-cure-for-ai-slop/README.md" ./README.md
rm -rf "$tmpdir"
```

Then re-apply any local edits you keep in `AGENTS.md`, `ATTRIBUTION.md`, or this file.

After you push to your GitHub remote, sync the same folder to Google Drive if you use Drive as a second pointer for bots.
