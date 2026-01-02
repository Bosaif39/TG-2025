# 🏆 True-Gaming Awards 2025 - Arabic Voting System

**An Arabic web application for [True-Gaming.net](https://www.true-gaming.net/boards/index.php) community voting system.**  
Users vote across multiple categories with a special "Best 5 Games of 2025" ranking category. Includes comprehensive admin dashboard with Excel export functionality.

*🎮 Designed specifically for gaming communities with full Arabic RTL support*

---

## 📁 Updated Project Structure

```
📦 TG-votes
├── static/
│   ├── css/
│   │   └── style.css           # Combined CSS for all pages
│   ├── js/
│   │   ├── admin.js            # Admin dashboard functionality
│   │   ├── index.js            # Main voting page logic
│   │   └── results.js          # Results display logic
├── templates/
│   ├── admin.html              # Admin dashboard interface
│   ├── index.html              # Main voting page
│   └── results.html            # Results display page
├── app.py                      # Main Flask application
├── game.txt                    # Initial game list database
├── votes.db                    # SQLite database (auto-generated)
├── requirements.txt            # Python dependencies
├── runtime.txt                 # Python version specification
├── render.yaml                 # Render deployment configuration
└── README.md                   # This file
```

---

## 🚀 Enhanced Features

### ✅ **Multi-Category Voting System**
* **8 Specialized Categories**: Best Expansion, Best Story, Best Art Direction, Best Music, Best Publisher, Best Surprise, Biggest Disappointment, Most Anticipated 2026
* **Main Ranking Category**: "أفضل ألعاب 2025" - Users rank their top 5 games with points (5,4,3,2,1)
* **Smart Autocomplete**: Separate suggestions for games and publishers based on category type

### ✅ **Advanced Admin Dashboard**
* **Multi-Table Management**: View/edit `categories`, `votes`, `games`, and `publishers` tables
* **Excel Export**: Download comprehensive voting results with multiple sheets
* **Real-time Editing**: Modify votes, games, publishers, and categories directly
* **Pagination & Search**: Navigate large datasets efficiently

### ✅ **Database Flexibility**
* **Dual Database Support**: SQLite for development, PostgreSQL for production
* **Automatic Migration**: Seamless switching between database types
* **Index Optimization**: Fast search and query performance

### ✅ **User Experience**
* **Arabic RTL Design**: Full right-to-left layout with Cairo font
* **Input Validation**: Sanitized inputs and duplicate vote prevention
* **Vote Verification**: Check if username has already voted
* **Personal Results**: View individual voting history

---

## 🧠 How The System Works

1. **User Registration**: Enter name → system checks if already voted
2. **Category Navigation**: Progress through 9 voting categories
3. **Smart Voting**:
   - Single selection for 8 categories (5 points each)
   - Ranked selection (5 games) for "Best Games 2025" category (5,4,3,2,1 points)
4. **Data Storage**: Votes saved with timestamps and calculated points
5. **Results Calculation**: Automatic aggregation by category and selection
6. **Admin Management**: Full CRUD operations on all data tables

---

## 🔐 Admin Dashboard Access

### Default Credentials:
- **Username**: `adminU`
- **Password**: `amdinSF` *(Change this in production!)*

### Access Steps:
1. Navigate to `/admin` on your deployed application
2. Enter the password
3. Access features:
   - **View Tables**: Browse categories, votes, games, publishers
   - **Edit Data**: Modify any entry directly
   - **Add New**: Create new games, publishers, or categories
   - **Export Excel**: Download complete voting data
   - **Delete Entries**: Remove unwanted data (with safeguards)

### Security Note:
The admin system uses session-based authentication with basic protection. For production use:
1. Change default credentials in `app.py`
2. Consider implementing proper user authentication
3. Use HTTPS in production
4. Restrict admin access by IP if possible

---

## 📊 Database Schema

### **Tables:**
1. **`categories`** - Voting categories with Arabic/English names
   ```sql
   id, name_ar, name_en, description, display_order
   ```

2. **`games`** - Game database for autocomplete
   ```sql
   id, name, created_at
   ```

3. **`publishers`** - Publisher database for "Best Publisher" category
   ```sql
   id, name, created_at
   ```

4. **`votes`** - User voting records
   ```sql
   id, voter_name, category_id, rank, selection, points, timestamp
   ```

### **Indexes:**
- Games/publishers names for fast autocomplete
- Votes by voter_name for quick lookup
- Votes by category_id for aggregation
- Votes by selection for ranking calculations

---

## 🧮 Voting & Points System

### **Category-Specific Rules:**

| Category Type | Selections Required | Points System | Example |
|--------------|---------------------|---------------|---------|
| **Best Games 2025** | 5 ranked games | 5,4,3,2,1 points | #1=5pts, #2=4pts, etc. |
| **Other Categories** | 1 selection each | 5 points fixed | Best Story = 5pts |

### **Ranking Calculation:**
```python
POINT_SYSTEM = {1: 5, 2: 4, 3: 3, 4: 2, 5: 1}
# Total points = SUM(points) across all voters
# Average rank = AVG(rank) across all voters
```

### **Excel Export Includes:**
1. **Category Rankings** - Top selections per category
2. **All Votes** - Complete voting records
3. **Games List** - All games in database
4. **Publishers List** - All publishers in database
5. **Summary Sheet** - System statistics and metrics

---
