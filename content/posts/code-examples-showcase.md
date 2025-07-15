+++
title = 'Code Examples Showcase'
date = 2025-07-15T09:51:59+08:00
draft = false
tags = ['programming', 'code', 'examples', 'tutorial']
categories = ['development']
summary = "A showcase of various programming languages and code snippets to demonstrate syntax highlighting and code block styling."
+++

This post demonstrates how different programming languages and code snippets look with our blog's styling. Let's explore various examples!
## JavaScript Examples

Here's a modern JavaScript function with async/await:

```javascript
async function fetchUserData(userId) {
  try {
    const response = await fetch(`/api/users/${userId}`);
    const userData = await response.json();
    
    if (!response.ok) {
      throw new Error(`HTTP error! status: ${response.status}`);
    }
    
    return {
      id: userData.id,
      name: userData.name,
      email: userData.email,
      createdAt: new Date(userData.created_at)
    };
  } catch (error) {
    console.error('Failed to fetch user data:', error);
    throw error;
  }
}

// Usage example
const user = await fetchUserData(123);
console.log(`Welcome, ${user.name}!`);
```

## Python Examples

A Python class demonstrating object-oriented programming:

```python
from typing import List, Optional
from dataclasses import dataclass
from datetime import datetime

@dataclass
class BlogPost:
    title: str
    content: str
    author: str
    created_at: datetime
    tags: List[str]
    published: bool = False
    
    def publish(self) -> None:
        """Publish the blog post."""
        self.published = True
        print(f"Published: {self.title}")
    
    def add_tag(self, tag: str) -> None:
        """Add a tag to the blog post."""
        if tag not in self.tags:
            self.tags.append(tag)
    
    def word_count(self) -> int:
        """Calculate the word count of the content."""
        return len(self.content.split())

# Create and use a blog post
post = BlogPost(
    title="My First Post",
    content="This is the content of my first blog post.",
    author="John Doe",
    created_at=datetime.now(),
    tags=["introduction", "blog"]
)

post.add_tag("python")
post.publish()
print(f"Word count: {post.word_count()}")
```

## Go Examples

A Go HTTP server with middleware:

```go
package main

import (
    "encoding/json"
    "fmt"
    "log"
    "net/http"
    "time"
)

type User struct {
    ID       int    `json:"id"`
    Name     string `json:"name"`
    Email    string `json:"email"`
    CreateAt time.Time `json:"created_at"`
}

func loggingMiddleware(next http.HandlerFunc) http.HandlerFunc {
    return func(w http.ResponseWriter, r *http.Request) {
        start := time.Now()
        next.ServeHTTP(w, r)
        log.Printf("%s %s %v", r.Method, r.URL.Path, time.Since(start))
    }
}

func getUserHandler(w http.ResponseWriter, r *http.Request) {
    user := User{
        ID:       1,
        Name:     "John Doe",
        Email:    "john@example.com",
        CreateAt: time.Now(),
    }
    
    w.Header().Set("Content-Type", "application/json")
    if err := json.NewEncoder(w).Encode(user); err != nil {
        http.Error(w, "Internal Server Error", http.StatusInternalServerError)
        return
    }
}

func main() {
    http.HandleFunc("/user", loggingMiddleware(getUserHandler))
    
    fmt.Println("Server starting on :8080")
    if err := http.ListenAndServe(":8080", nil); err != nil {
        log.Fatal("Server failed to start:", err)
    }
}
```

## React/TypeScript Example

A modern React component with TypeScript:

```typescript
import React, { useState, useEffect } from 'react';

interface User {
  id: number;
  name: string;
  email: string;
}

interface UserListProps {
  apiUrl: string;
  onUserSelect?: (user: User) => void;
}

const UserList: React.FC<UserListProps> = ({ apiUrl, onUserSelect }) => {
  const [users, setUsers] = useState<User[]>([]);
  const [loading, setLoading] = useState<boolean>(true);
  const [error, setError] = useState<string | null>(null);

  useEffect(() => {
    const fetchUsers = async () => {
      try {
        setLoading(true);
        const response = await fetch(apiUrl);
        
        if (!response.ok) {
          throw new Error(`Failed to fetch users: ${response.statusText}`);
        }
        
        const userData = await response.json();
        setUsers(userData);
      } catch (err) {
        setError(err instanceof Error ? err.message : 'Unknown error');
      } finally {
        setLoading(false);
      }
    };

    fetchUsers();
  }, [apiUrl]);

  if (loading) return <div className="loading">Loading users...</div>;
  if (error) return <div className="error">Error: {error}</div>;

  return (
    <div className="user-list">
      <h2>Users</h2>
      {users.map(user => (
        <div 
          key={user.id} 
          className="user-item"
          onClick={() => onUserSelect?.(user)}
        >
          <h3>{user.name}</h3>
          <p>{user.email}</p>
        </div>
      ))}
    </div>
  );
};

export default UserList;
```

## CSS Examples

Modern CSS with Grid and Flexbox:

```css
/* Modern CSS Grid Layout */
.blog-layout {
  display: grid;
  grid-template-columns: 1fr 3fr 1fr;
  grid-template-rows: auto 1fr auto;
  grid-template-areas: 
    "header header header"
    "sidebar main aside"
    "footer footer footer";
  min-height: 100vh;
  gap: 1rem;
}

.header {
  grid-area: header;
  background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
  color: white;
  padding: 2rem;
  text-align: center;
}

.sidebar {
  grid-area: sidebar;
  background: #f8f9fa;
  padding: 1rem;
  border-radius: 0.5rem;
}

.main-content {
  grid-area: main;
  padding: 2rem;
}

/* Responsive Card Component */
.card {
  background: white;
  border-radius: 0.75rem;
  box-shadow: 0 4px 6px -1px rgba(0, 0, 0, 0.1);
  padding: 1.5rem;
  transition: transform 0.2s ease, box-shadow 0.2s ease;
}

.card:hover {
  transform: translateY(-2px);
  box-shadow: 0 10px 25px -3px rgba(0, 0, 0, 0.1);
}

@media (max-width: 768px) {
  .blog-layout {
    grid-template-columns: 1fr;
    grid-template-areas: 
      "header"
      "main"
      "sidebar"
      "footer";
  }
}
```

## SQL Examples

Complex database queries:

```sql
-- Complex JOIN query with window functions
WITH user_stats AS (
  SELECT 
    u.id,
    u.name,
    u.email,
    COUNT(p.id) as post_count,
    AVG(p.view_count) as avg_views,
    ROW_NUMBER() OVER (ORDER BY COUNT(p.id) DESC) as rank
  FROM users u
  LEFT JOIN posts p ON u.id = p.author_id
  WHERE u.created_at >= '2024-01-01'
    AND u.active = true
  GROUP BY u.id, u.name, u.email
),
top_authors AS (
  SELECT *
  FROM user_stats
  WHERE rank <= 10
)
SELECT 
  ta.name,
  ta.email,
  ta.post_count,
  ROUND(ta.avg_views, 2) as avg_views,
  ta.rank,
  CASE 
    WHEN ta.post_count >= 50 THEN 'Prolific'
    WHEN ta.post_count >= 20 THEN 'Active'
    WHEN ta.post_count >= 5 THEN 'Regular'
    ELSE 'New'
  END as author_level
FROM top_authors ta
ORDER BY ta.rank;
```

## Bash/Shell Examples

Useful shell scripts:

```bash
#!/bin/bash

# Blog deployment script
set -e  # Exit on any error

# Configuration
BLOG_DIR="/var/www/blog"
BACKUP_DIR="/var/backups/blog"
HUGO_VERSION="0.128.0"

# Colors for output
RED='\033[0;31m'
GREEN='\033[0;32m'
YELLOW='\033[1;33m'
NC='\033[0m' # No Color

log() {
    echo -e "${GREEN}[$(date +'%Y-%m-%d %H:%M:%S')] $1${NC}"
}

error() {
    echo -e "${RED}[ERROR] $1${NC}" >&2
}

warning() {
    echo -e "${YELLOW}[WARNING] $1${NC}"
}

# Function to check if Hugo is installed
check_hugo() {
    if ! command -v hugo &> /dev/null; then
        error "Hugo is not installed"
        exit 1
    fi
    
    local version=$(hugo version | grep -oE 'v[0-9]+\.[0-9]+\.[0-9]+')
    log "Hugo version: $version"
}

# Function to backup current site
backup_site() {
    if [ -d "$BLOG_DIR" ]; then
        log "Creating backup..."
        local backup_name="blog_backup_$(date +%Y%m%d_%H%M%S)"
        cp -r "$BLOG_DIR" "$BACKUP_DIR/$backup_name"
        log "Backup created: $BACKUP_DIR/$backup_name"
    fi
}

# Function to deploy blog
deploy_blog() {
    log "Starting blog deployment..."
    
    # Pull latest changes
    git pull origin main
    
    # Install dependencies if package.json exists
    if [ -f "package.json" ]; then
        log "Installing npm dependencies..."
        npm ci
    fi
    
    # Build the site
    log "Building Hugo site..."
    hugo --gc --minify
    
    # Copy to web directory
    log "Deploying to $BLOG_DIR..."
    rsync -av --delete public/ "$BLOG_DIR/"
    
    # Set proper permissions
    chown -R www-data:www-data "$BLOG_DIR"
    chmod -R 755 "$BLOG_DIR"
    
    log "Deployment completed successfully!"
}

# Main execution
main() {
    log "Blog deployment script started"
    
    check_hugo
    backup_site
    deploy_blog
    
    log "All operations completed successfully!"
}

# Run main function
main "$@"
```

## Inline Code Examples

Sometimes you need to reference code inline, like `const variable = 'value'` or `npm install package-name`. You can also mention file paths like `/etc/nginx/nginx.conf` or commands like `sudo systemctl restart nginx`.

## Code with Comments

Here's a well-commented function:

```python
def fibonacci_memoized(n: int, memo: dict = None) -> int:
    """
    Calculate the nth Fibonacci number using memoization.
    
    Args:
        n (int): The position in the Fibonacci sequence
        memo (dict, optional): Memoization cache
    
    Returns:
        int: The nth Fibonacci number
    
    Time Complexity: O(n)
    Space Complexity: O(n)
    """
    if memo is None:
        memo = {}
    
    # Base cases
    if n <= 1:
        return n
    
    # Check if already computed
    if n in memo:
        return memo[n]
    
    # Compute and store result
    memo[n] = fibonacci_memoized(n - 1, memo) + fibonacci_memoized(n - 2, memo)
    return memo[n]

# Example usage
for i in range(10):
    print(f"F({i}) = {fibonacci_memoized(i)}")
```

This showcase demonstrates how various programming languages and code snippets appear with our blog's styling. The syntax highlighting and formatting should make code easy to read and understand!