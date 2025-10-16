# Admin Mode Implementation - Issue #5

## Changes Made

### 1. Backend Changes (app.py)
- Added authentication imports: `Depends`, `Header`, `BaseModel`, `json`, `Optional`
- Created `teachers.json` loading function
- Added in-memory session storage for authenticated teachers
- Created `LoginRequest` Pydantic model for login requests
- Added `verify_teacher()` authentication helper function
- Added `/login` endpoint for teacher authentication
- Added `/logout` endpoint for teacher logout
- Protected `/activities/{activity_name}/signup` endpoint - now requires authentication
- Protected `/activities/{activity_name}/unregister` endpoint - now requires authentication

### 2. Frontend Changes (index.html)
- Added user controls in header (Login button and user info display)
- Added login modal with username/password form
- Made signup container "teacher-only" and hidden by default
- Added error message display for login failures

### 3. JavaScript Changes (app.js)
- Added authentication state management using localStorage
- Added login modal show/hide functionality
- Added login form submission handler
- Added logout functionality
- Added `updateAuthUI()` function to show/hide elements based on auth state
- Modified participant list to only show delete buttons for authenticated teachers
- Added Authorization header to signup and unregister API calls
- Delete buttons now only appear when logged in

### 4. CSS Changes (styles.css)
- Added styles for user controls in header (positioned top-right)
- Added modal styles for login dialog
- Added styles for login button and user info display
- Added styles for logout button
- Responsive positioning for user controls

### 5. New File Created
- `teachers.json` - Contains teacher credentials (username/password pairs)
  - admin/admin123
  - teacher1/password123
  - teacher2/password456

## How It Works

1. **Students (Not Logged In)**:
   - Can view all activities
   - Can see participant lists
   - Cannot see delete buttons
   - Cannot see signup form
   - See "Login" button in top-right

2. **Teachers (Logged In)**:
   - See their username in top-right
   - Can register students for activities
   - Can unregister students from activities
   - See delete buttons next to participants
   - Can logout

## Security Notes
- Sessions are stored in memory (will reset on server restart)
- Passwords are stored in plain text (for simplicity, as per issue requirements)
- In production, you should use:
  - JWT tokens or secure session management
  - Password hashing (bcrypt)
  - HTTPS
  - Database-backed session storage
