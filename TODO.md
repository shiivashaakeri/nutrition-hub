# Nutrition Hub v7 - Complete TODO List

## Overview
This document outlines all features, fixes, and improvements to be implemented.
Check off items as completed: [ ] → [x]

---

## 🔴 PHASE 1: Critical Bug Fixes

### 1.1 Sleep Persistence Bug
- [x] **Root cause**: `todayData.sleep` saves but doesn't reload properly
- [x] Add `console.log` to debug data flow (temporary)
- [x] Ensure `todayData` merges correctly with Firebase data on load
- [x] Verify `renderSleep()` is called AFTER data loads
- [x] Added localStorage backup for data safety
- [ ] Test: Log sleep → Refresh → Should persist

### 1.2 Weekly Stats Timing Bug  
- [x] **Root cause**: `renderWeeklyMiniStats()` runs before `history` loads
- [x] Move `renderWeeklyMiniStats()` call to AFTER `loadAllData()` completes
- [x] Add null checks in `getWeekData()` function
- [x] Ensure `history` array is populated before rendering
- [x] Added debug logging to trace issues
- [ ] Test: Refresh page → Weekly stats show immediately (not "--")

### 1.3 History Array Sync
- [x] When `saveToday()` runs, update `history` array in memory
- [x] Ensure calendar reads from updated history
- [x] Add realtime listener to update history when other tabs change data

---

## 🟠 PHASE 2: Day Detail Page (New Feature)

### 2.1 Create Day Page Structure
- [ ] Create new file: `day.html`
- [ ] URL structure: `day.html?date=2026-01-03`
- [ ] Header with back button and date display
- [ ] Date navigation (prev/next day arrows)

### 2.2 Day Summary Section
- [ ] Large protein/calories/sleep display cards
- [ ] Visual progress rings for protein & calories
- [ ] Goal completion indicators (✓ or remaining)
- [ ] Color coding: green=hit, orange=close, red=missed

### 2.3 Foods Section
- [ ] List all foods logged that day
- [ ] Each food item shows: emoji, name, protein, calories
- [ ] Edit button on each food → opens edit modal
- [ ] Delete button on each food (with confirmation)
- [ ] "Add Food" button → opens food picker (reuse from today.html)
- [ ] Support adding foods to ANY day, not just today

### 2.4 Workout Section
- [ ] Show workout name, duration, icon
- [ ] List all exercises with sets/reps/weight
- [ ] Edit workout button → opens workout editor
- [ ] Add workout button if none logged
- [ ] Delete workout button

### 2.5 Supplements Section
- [ ] Morning/Evening toggle buttons
- [ ] Click to toggle on/off
- [ ] Save changes immediately

### 2.6 Sleep Section  
- [ ] Display current sleep hours
- [ ] Edit button → opens sleep input modal
- [ ] Save immediately

### 2.7 Notes Section (New!)
- [ ] Text area for daily notes/reflections
- [ ] Auto-save as you type (debounced)
- [ ] Character limit: 500
- [ ] Store in `todayData.notes`

### 2.8 Navigation Integration
- [ ] Calendar day click → navigates to day.html?date=X
- [ ] "View Day" button in day detail popup
- [ ] Back button returns to previous page

---

## 🟡 PHASE 3: Week Dashboard (New Feature)

### 3.1 Create Week Page Structure
- [ ] Create new file: `week.html`
- [ ] URL structure: `week.html?start=2026-01-01`
- [ ] Header with week range display
- [ ] Week navigation (prev/next week)

### 3.2 Week Overview Bar
- [ ] 7-day horizontal bar showing each day
- [ ] Color indicators: green=goal hit, orange=partial, gray=no data
- [ ] Protein amount below each day
- [ ] Workout icon (💪) on workout days
- [ ] Click day → navigates to day.html

### 3.3 Weekly Stats Section
- [ ] Average protein (calculated from days WITH data)
- [ ] Total calories for week
- [ ] Workout count / planned
- [ ] Average sleep
- [ ] Goals hit count (X/7)
- [ ] Compare to previous week (↑ or ↓ indicators)

### 3.4 Weekly Highlights
- [ ] Best day (highest protein)
- [ ] Longest workout
- [ ] Any PRs set this week
- [ ] Streak status

### 3.5 Weekly Notes Section
- [ ] Text area for weekly reflection
- [ ] Prompts: "What went well?", "What to improve?"
- [ ] Store in separate Firebase doc: `users/{uid}/weeks/{weekId}`

### 3.6 Week Actions
- [ ] "Copy to This Week" - copy meal plan from another week
- [ ] "Export Week" - download as image/PDF
- [ ] Navigate to any day within the week

### 3.7 Integration with Today Page
- [ ] "This Week" card links to week.html
- [ ] Show mini stats on card (as already exists)
- [ ] Fix timing so stats show immediately

---

## 🟢 PHASE 4: Enhanced Calendar

### 4.1 Calendar Views
- [ ] Add view toggle: [Day] [Week] [Month] [List]
- [ ] Day view: Shows single day detail (→ day.html)
- [ ] Week view: Shows week dashboard (→ week.html)  
- [ ] Month view: Current calendar grid (enhanced)
- [ ] List view: Scrollable list of all logged days

### 4.2 Enhanced Month Calendar
- [ ] Larger day cells with more info
- [ ] Show protein amount in each cell
- [ ] Workout indicator (small icon)
- [ ] Sleep indicator (if tracked)
- [ ] Heat map coloring based on goal %

### 4.3 Quick Actions (Long Press / Right Click)
- [ ] "Copy this day" → copies to clipboard
- [ ] "Paste day" → paste copied day's data
- [ ] "Log same as yesterday" → quick duplicate
- [ ] "Mark as rest day" → special tag
- [ ] "Add note" → quick note entry

### 4.4 Calendar Legend (Enhanced)
- [ ] 🟢 Goal hit (100%+)
- [ ] 🟡 Close (80-99%)
- [ ] 🟠 Partial (50-79%)
- [ ] 🔴 Missed (<50%)
- [ ] ⚪ No data
- [ ] 💪 Workout logged
- [ ] 😴 Sleep tracked

---

## 🔵 PHASE 5: Data Safety & Sync

### 5.1 Local Storage Backup
- [ ] Save `todayData` to localStorage on every change
- [ ] On page load, check localStorage first
- [ ] If localStorage is newer than Firebase, use localStorage
- [ ] Sync to Firebase in background
- [ ] Clear localStorage after successful sync

### 5.2 Offline Support
- [ ] Detect offline status
- [ ] Queue changes when offline
- [ ] Sync queue when back online
- [ ] Show "Offline" indicator in header

### 5.3 Sync Status Indicator
- [ ] "Saving..." during save
- [ ] "Saved ✓" after successful save
- [ ] "Offline - will sync" when offline
- [ ] "Sync error" with retry button

### 5.4 Undo/Redo System
- [ ] Track last 5 actions in memory
- [ ] "Undo" button appears after action
- [ ] Auto-hides after 5 seconds
- [ ] Actions: add food, delete food, edit food, log workout

### 5.5 Data Export
- [ ] Export single day as image
- [ ] Export week as PDF
- [ ] Export all data as CSV
- [ ] Export all data as JSON (backup)

---

## 🟣 PHASE 6: Food Logging Improvements

### 6.1 Meal Templates
- [ ] Create "My Meals" section in Food page
- [ ] Save meal template: name + list of foods
- [ ] One-tap to log entire meal
- [ ] Edit/delete templates
- [ ] Store in: `users/{uid}/data/mealTemplates`

### 6.2 Quick Actions
- [ ] "Copy yesterday" button on Today page
- [ ] "Log same breakfast" quick action
- [ ] Favorites bar: top 5 most-used foods
- [ ] Recent foods with frequency indicator

### 6.3 Quick Macro Entry
- [ ] "Quick add" button
- [ ] Just enter: protein, calories (no food name)
- [ ] Logged as "Quick entry - 30g protein"
- [ ] Useful for eating out / estimates

### 6.4 Food Search Improvements
- [ ] Search by protein amount ("high protein")
- [ ] Filter by category while searching
- [ ] Recently searched terms
- [ ] "Did you mean..." suggestions

### 6.5 Edit Food on Any Day
- [ ] When on day.html, food edits save to THAT day
- [ ] Not just today - any historical day
- [ ] Recalculate daily totals after edit

---

## ⚫ PHASE 7: Workout Improvements

### 7.1 Edit Past Workouts
- [ ] Full edit capability in workout detail modal
- [ ] Edit exercise name, sets, reps, weight
- [ ] Add/remove exercises from past workout
- [ ] Save changes to Firebase

### 7.2 Workout Templates
- [ ] Save current workout as template
- [ ] "My Routines" section in Gym page
- [ ] Start workout from template
- [ ] Edit templates

### 7.3 Exercise Library
- [ ] Comprehensive exercise database
- [ ] Search by muscle group
- [ ] Search by equipment
- [ ] Custom exercise creation
- [ ] Exercise instructions/tips

### 7.4 During Workout Features
- [ ] Rest timer between sets
- [ ] Auto-start timer after logging set
- [ ] Customizable rest duration
- [ ] Sound/vibration notification

### 7.5 Superset Support
- [ ] Group exercises as superset
- [ ] Display grouped in workout log
- [ ] Superset templates

---

## ⬜ PHASE 8: Analytics & Insights

### 8.1 Progress Charts (Enhanced)
- [ ] Protein trend (7/30/90 days)
- [ ] Calorie trend
- [ ] Weight trend (if tracking)
- [ ] Workout frequency chart
- [ ] Sleep trend

### 8.2 Correlations & Insights
- [ ] "You hit goals more on days you sleep 7+ hrs"
- [ ] "Your protein is highest on Mondays"
- [ ] "You've been consistent for X weeks"
- [ ] Weekly improvement percentage

### 8.3 Goal Predictions
- [ ] "At this rate, you'll reach X by [date]"
- [ ] Weight goal projection
- [ ] Streak prediction

### 8.4 Comparisons
- [ ] This week vs last week
- [ ] This month vs last month
- [ ] Best week ever
- [ ] Personal records summary

---

## 🔲 PHASE 9: Quality of Life

### 9.1 Daily Notes System
- [ ] Notes field on every day
- [ ] Quick note from Today page
- [ ] View notes in calendar (indicator)
- [ ] Search notes

### 9.2 Day Tags
- [ ] Predefined tags: vacation, sick, rest day, competition, travel
- [ ] Custom tags
- [ ] Filter calendar by tag
- [ ] Tag statistics

### 9.3 Progress Photos
- [ ] Upload photo linked to date
- [ ] Photo gallery view
- [ ] Compare photos side-by-side
- [ ] Store in Firebase Storage

### 9.4 Mood/Energy Tracker
- [ ] Rate energy 1-5 each day
- [ ] Rate mood 1-5 each day
- [ ] Correlate with sleep/nutrition
- [ ] Simple emoji selection

### 9.5 Reminders/Notifications
- [ ] Daily logging reminder
- [ ] Protein goal check-in
- [ ] Workout reminder
- [ ] Supplement reminder
- [ ] (Requires service worker / push notifications)

---

## 📋 PHASE 10: Code Quality & Polish

### 10.1 Code Organization
- [ ] Extract shared functions to `utils.js`
- [ ] Create `firebase-helpers.js` for DB operations
- [ ] Consistent naming conventions
- [ ] Add code comments

### 10.2 Performance
- [ ] Lazy load modals
- [ ] Debounce search inputs
- [ ] Optimize Firebase queries
- [ ] Reduce bundle size

### 10.3 Error Handling
- [ ] Try/catch on all async operations
- [ ] User-friendly error messages
- [ ] Automatic retry on failure
- [ ] Error logging

### 10.4 Accessibility
- [ ] Proper ARIA labels
- [ ] Keyboard navigation
- [ ] Screen reader support
- [ ] Color contrast check

### 10.5 Testing
- [ ] Test on iOS Safari
- [ ] Test on Android Chrome
- [ ] Test offline mode
- [ ] Test with slow connection

---

## 📊 Implementation Order

### Sprint 1: Bug Fixes (CURRENT)
1. [ ] 1.1 Sleep persistence
2. [ ] 1.2 Weekly stats timing
3. [ ] 1.3 History sync

### Sprint 2: Day Detail Page
1. [ ] 2.1-2.2 Page structure & summary
2. [ ] 2.3 Foods section with edit
3. [ ] 2.4-2.6 Workout, supplements, sleep
4. [ ] 2.7-2.8 Notes & navigation

### Sprint 3: Week Dashboard
1. [ ] 3.1-3.2 Structure & overview
2. [ ] 3.3-3.4 Stats & highlights
3. [ ] 3.5-3.7 Notes & integration

### Sprint 4: Data Safety
1. [ ] 5.1-5.2 Local storage & offline
2. [ ] 5.3-5.4 Sync indicator & undo
3. [ ] 5.5 Export

### Sprint 5: Enhanced Features
1. [ ] 4.1-4.4 Calendar enhancements
2. [ ] 6.1-6.5 Food improvements
3. [ ] 7.1-7.5 Workout improvements

### Sprint 6: Analytics & Polish
1. [ ] 8.1-8.4 Analytics
2. [ ] 9.1-9.5 Quality of life
3. [ ] 10.1-10.5 Code quality

---

## 📝 Notes

- Each phase builds on the previous
- Test thoroughly after each sprint
- Get user feedback between sprints
- Prioritize based on daily usage impact

---

## 🎯 Success Metrics

- [ ] Sleep persists 100% of the time
- [ ] Weekly stats load instantly
- [ ] Can edit any past day
- [ ] Works offline
- [ ] No data loss ever
- [ ] Page load < 2 seconds

---

*Last updated: January 3, 2026*
*Version target: v7.0*
