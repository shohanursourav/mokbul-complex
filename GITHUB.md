# GitHub এ আপলোড করার নিয়ম

প্রজেক্টটা এখন GitHub-এর জন্য তৈরি। `index.html`, `assets/`, `README.md` এই তিনটাই যথেষ্ট।

---

## উপায় ১: ওয়েবসাইট থেকে ড্র্যাগ অ্যান্ড ড্রপ (সবচেয়ে সহজ)

1. [github.com/new](https://github.com/new) এ যান
2. Repository name: `mokbul-complex`
3. Public রাখুন (GitHub Pages ফ্রি পেতে হলে Public দরকার)
4. **Create repository** চাপুন
5. পরের পেজে **uploading an existing file** লিংকে ক্লিক করুন
6. zip ফাইলটা খুলে ভেতরের সব ফাইল ( `index.html`, `README.md`, `.gitignore`, `GITHUB.md` এবং পুরো `assets` ফোল্ডার ) ড্র্যাগ করে ছেড়ে দিন
7. নিচে **Commit changes** চাপুন

> ফোল্ডার ড্র্যাগ করলে GitHub নিজেই ভেতরের ফাইলগুলো নিয়ে নেয়। মোট ৭টি ফাইল: `index.html`, `README.md`, `.gitignore`, `GITHUB.md` এবং `assets/` এর ভেতরে ৬টি ছবি।

---

## উপায় ২: টার্মিনাল / Git কমান্ড

zip ফাইলটা খুলে `mokbul-complex` ফোল্ডারে ঢুকে এই কমান্ডগুলো দিন:

```bash
git init -b main
git add .
git commit -m "Mokbul Complex website"
git remote add origin https://github.com/USERNAME/mokbul-complex.git
git push -u origin main
```

`USERNAME` এর জায়গায় আপনার GitHub ইউজারনেম বসান। পাসওয়ার্ড চাইলে
**Personal Access Token** ব্যবহার করুন (Settings → Developer settings → Tokens)।

### GitHub CLI থাকলে এক লাইনেই হয়ে যাবে

```bash
gh repo create mokbul-complex --public --source=. --remote=origin --push
```

---

## লাইভ সাইট বানানো (GitHub Pages, ফ্রি)

1. রিপোতে **Settings → Pages** এ যান
2. **Source**: Deploy from a branch
3. **Branch**: `main`, ফোল্ডার: `/ (root)` → **Save**
4. ১ মিনিট পর সাইট চালু হবে:
   `https://USERNAME.github.io/mokbul-complex/`

সব ছবির পথ relative (`assets/...`) দেওয়া আছে, তাই Pages-এ কোনো কিছু বদলাতে হবে না।

### নিজের ডোমেইন লাগলে
Settings → Pages → Custom domain এ ডোমেইনটা দিন, তারপর ডোমেইনের DNS-এ
`CNAME` রেকর্ড যোগ করুন: `USERNAME.github.io`

---

## হালনাগাদ করার নিয়ম

ফাইল বদলানোর পর:

```bash
git add .
git commit -m "কী বদলালো তার সংক্ষিপ্ত বিবরণ"
git push
```

Pages নিজে থেকেই নতুন ভার্সন দেখাবে।

---

## খেয়াল রাখুন

- অ্যাপের ভেতরের `assets/` ফোল্ডারের নাম বদলাবেন না, নাহলে ছবি লোড হবে না।
- ফোন নম্বর, ঠিকানা বা অন্য কিছু বদলাতে চাইলে `index.html`-এর নিচের `SITE` অংশটাই বদলান।
- ভবিষ্যতে ছবি বদলাতে চাইলে একই নামে (`building-corner.jpg` ইত্যাদি) ফাইল ওভাররাইট করুন।
