## 🧠 JavaScript API Exercises

This assignment has **two parts** — one for practicing a GET request to display posts, and another for building your own API-based app.

---

## 🧩 **Part 1: Display Posts from JSONPlaceholder (GET Request)**

You already have a file named **`index.html`** with all the HTML and JavaScript comments included. Your goal is to complete the JavaScript that’s already written in the `<script>` section.

### 🎯 **Goal:**

Fetch posts from the following API and display them on the page as Bootstrap cards:

```
https://jsonplaceholder.typicode.com/posts
```

### ✅ **Instructions:**

1. Inside the `loadPosts()` function, replace the static `postsData` array with a `fetch()` call to the API above.


### ⚡ **Challenge:**

* Replace the static Lego image with random cat images using this API:

  ```
  https://api.thecatapi.com/v1/images/search
  ```

  Fetch one new image URL for each post card.
* Limit your output to only **10–15 posts** by adjusting the for-loop condition.

💡 *All required instructions are already embedded as comments in your HTML file — follow them carefully and complete the code.*

---

## 🎬 **Part 2: OMDb Movie Search (GET Request)**

Build a simple movie search page using the **OMDb API**.

You already have a **blank HTML page** with a **text box**, a **Search button**, and an empty `script.js`. Students must write **all JavaScript**.

### 🎯 Goal

When the user types a movie name and clicks **Search**:

1. Fetch data from OMDb using your API key
2. Display the movie’s **Title, Year, Genre, Plot, and Poster** in the page

### ✅ Steps

#### Step 1 – Get an API Key

1. Go to [https://www.omdbapi.com/apikey.aspx](https://www.omdbapi.com/apikey.aspx)
2. Register for a **free** key (1,000 requests/day)
3. In `script.js`, store it:

```js
const apiKey = "YOUR_API_KEY_HERE";
```

#### Step 2 – Read Input & Build URL

```js
const movieName = document.getElementById('movieInput').value.trim();
const type = document.getElementById('typeSelect') ? document.getElementById('typeSelect').value : '';
const url = `https://www.omdbapi.com/?apikey=${apiKey}&t=${encodeURIComponent(movieName)}&type=${type}`;
```

#### Step 3 – Fetch & Handle Response

```js
fetch(url)
  .then(res => res.json())
  .then(data => {
    const result = document.getElementById('result');

    if (data.Response === 'False') {
      result.innerHTML = `<p style="color:red;">❌ ${data.Error || 'Movie not found.'}</p>`;
      return;
    }

    result.innerHTML = `
      <div style="display:flex; gap:16px; align-items:flex-start;">
        <img src="${data.Poster}" alt="Poster" width="160" onerror="this.src=''">
        <div>
          <h2>${data.Title} (${data.Year})</h2>
          <p><strong>Genre:</strong> ${data.Genre}</p>
          <p><strong>Rated:</strong> ${data.Rated}</p>
          <p><strong>IMDB:</strong> ${data.imdbRating}</p>
          <p>${data.Plot}</p>
        </div>
      </div>`;
  })
  .catch(err => {
    console.error(err);
    document.getElementById('result').innerHTML = '<p style="color:red;">❌ Network error. Try again.</p>';
  });
```

### 🧪 Expected Behavior

* ✅ Valid movie → details render in the page
* ❌ Invalid/empty input → show a clear error message

### ⚡ Challenges (Optional)

* Add a **dropdown** to filter by `movie`, `series`, or `episode` and include it via `&type=` in the URL
* Show a **loading…** message while fetching
