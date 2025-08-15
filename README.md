# wiki.

**wiki.** is a simple website that lets you search for and read Wikipedia articles.  
It's designed to feel fast and easy to use — without all the extra stuff on the full Wikipedia site.

---

## How It Works

This project is just **one file** — it contains the look of the website, the content on the page, and the instructions for how everything works.

### Main Parts of the Website

#### 1. Getting Info from Wikipedia
The code talks to Wikipedia’s public API to get search results and articles.  
It uses `fetch` to request the needed data.

```javascript
const fetchArticle = async (title) => {
    try {
        const response = await fetch(
            `https://en.wikipedia.org/w/api.php?action=parse&format=json&origin=*&page=${encodeURIComponent(title)}`
        );
        // ...
    } catch (error) {
        console.error('Failed to fetch article:', error);
    }
};
```

#### 2. Making the Page Appear
When you search or click an article, the code builds the page in your browser — adding and removing parts as needed.

#### 3. Custom Look and Feel
The site includes effects like a glowing, moving grid and a custom cursor, animated with simple CSS/JavaScript.

---

## Why the Code Is Hard to Fix

If the code feels messy or confusing, you’re not wrong.

**Here’s why:**

- **Everything is in one place**  
  Imagine writing a book where all the chapters, notes, and character lists are jumbled together. That’s what this code is like — a single long file that’s hard to follow.

- **No clear sections**  
  Search logic, article display, and animations all live in the same space, making it easy for things to get tangled.

- **Manually building the page**  
  The code manually tells the browser where every button and text goes. It’s like building a house brick-by-brick with your bare hands instead of using prefabricated parts.

```javascript
const renderSuggestions = (suggestions) => {
    searchResults.innerHTML = '';
    suggestions.forEach(title => {
        const li = document.createElement('li');
        li.textContent = title;
        li.className = '...';
        li.addEventListener('click', () => { /* ... */ });
        searchResults.appendChild(li);
    });
};
```

---

## How to Make It Better

### 1. Use a Modern Framework
React or Next.js are like special machines for building websites — they let you create reusable “pieces” that fit together.

**Example:** A Search Bar in React:

```javascript
import React, { useState, useEffect } from 'react';

const SearchBar = ({ onSelect }) => {
    const [query, setQuery] = useState('');
    const [suggestions, setSuggestions] = useState([]);

    useEffect(() => {
        // Debounced fetch call here...
    }, [query]);

    return (
        <div className="w-full relative">
            <input
                type="text"
                value={query}
                onChange={(e) => setQuery(e.target.value)}
                placeholder="Search Wikipedia..."
            />
            <ul className="absolute top-full ...">
                {suggestions.map((title) => (
                    <li key={title} onClick={() => onSelect(title)}>
                        {title}
                    </li>
                ))}
            </ul>
        </div>
    );
};
```

---

### 2. Separate the Code
- Put search logic in `search.js`  
- Put article display in `article.js`  
- Put animations in `animations.js`  

This way, you can fix or improve one part without breaking everything else.

---

### 3. Let the Framework Do the Work
In React (or similar), you **describe** what you want, and it updates the page automatically when data changes.  
_No more manually adding/removing elements._

---

## What to Do Next

1. Learn React (or Next.js) — both solve the problems in this project.  
2. Refactor the current code into smaller files.  
3. Replace manual DOM updates with framework components.  

> 💡 **Tip:** You can run this project by simply opening the file in a browser.
