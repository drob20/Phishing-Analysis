# Phishing-Analysis# 1) copy uploaded docx into working folder (adjust path if needed)
cp /mnt/data/0e3b5c29-8ce0-4a64-b191-a1f6076f862a.docx ./tools/original_analysis.docx

# 2) convert to markdown
pandoc ./tools/original_analysis.docx -f docx -t gfm -o ./phishing/2025-11-02_saintleo_vibeaccount_analysis.md

# 3) prepend front-matter (date, title, source, classification)
cat > ./phishing/frontmatter.tmp <<'EOF'
---
title: "SAINTLEO / vibeaccount phishing — analysis"
date: 2025-11-02
source: "student-email (redacted)"
classification: "phishing"
references: ["uploaded original DOCX"]
---
EOF

# join header + converted doc
cat ./phishing/frontmatter.tmp ./phishing/2025-11-02_saintleo_vibeaccount_analysis.md > ./phishing/tmp && mv ./phishing/tmp ./phishing/2025-11-02_saintleo_vibeaccount_analysis.md && rm ./phishing/frontmatter.tmp
