# Haus: Co-living made easy

## Vision
> To make co-living easy so that, renters not only enjoy living with others, they prefer it.

## Mission
> To create a world where anyone can live together.

## Description
> Most people don’t dislike living with roommates, they dislike living with the wrong ones. Haus is a cross-platform web and mobile app that helps guarantee renters find the right roommate and are equipped with the tools they need to manage living together.
>
> Whether you are searching for a replacement, moving across the country, or renting for the first time, Haus will give you the confidence to form your next household.

---

## 📖 Table of Contents
- [Features](#-features)
- [Design & UI/UX](#-design--uiux)
- [Tech Stack](#-tech-stack)
- [Getting Started](#-getting-started)
- [Usage](#-usage)
- [Contributing](#-contributing)
- [License](#-license)

---

## ✨ Features

- **Platform Design:**
    - **Intuitive UI Design:** Adhere mostly to original Figma designs. For any undocumented edge cases or UX flows, default to [Airbnb’s](//www.airbnb.com) design patterns (spacing, information density, and navigation flow).
    - **Responsive Mobile Design:** Use a mobile-first breakpoint strategy. Prioritize the layout for mobile web and native-wrapped views (WebView, iOS UIView, Android View) before scaling up to tablet and desktop.
    - **Dynamic Component System:** Build modular UI elements using a "Single Source of Truth" for styles. All components must pull from the established design tokens (e.g., $radius-lg, $shadow-soft, etc.) rather than using hardcoded values. Consistency over custom one-offs.
    - **Dynamic Color Themes:** Implement a theme-provider system. All styling must support dynamic color injections for Light Mode, Dark Mode, and white-label overrides without requiring CSS overrides.
    - **Smooth UI Animations:** Use a "physics-based" micro-interaction model. Focus on state transitions (entry/exit, button presses, and list loading) rather than decorative loops. Optimize for touch-start latency on mobile. Ensure animations are interruptible and respect prefers-reduced-motion settings.
        - Implement a "Tactile & Spatial" motion model. Move beyond basic fades; use Shared Element Transitions (e.g., an image morphing into a header) to maintain user context between views.
        - Use high-tension Spring Physics (overshoot and squash) for all interactive elements. Buttons should feel "elastic" rather than mechanical, responding to the velocity of the user's gesture.
        - Use Z-axis depth for layers. New views should feel like they are sliding over or expanding from the point of interaction, creating a 3D mental map of the app.
        - Apply subtle scale-down effects (e.g., 95%) on press to simulate physical resistance.
        - Avoid generic spinners; use shimmering "skeleton" loaders or custom path-morphing SVG animations that reflect the brand's shape language.
        - All animations must be hardware-accelerated (60fps+) and interruptible—users should be able to "catch" a transition mid-way and reverse it with a gesture.
- **Header Section:** Build single-row header component with configurable left/center/right options and actions: title text, back button, notifications button, settings menu, filter button, cancel button, ellipses button
    - **Header Logic:** The header must be dynamically configurable based on the active route. Left: Navigation & Title (Back, Cancel, Title). Right: Contextual Actions (Save, Notifications, Settings, Filters, Ellipses). Support "Sticky" positioning with backdrop-blur effects on scroll.
    - **Header Badges:** Implement a reactive "Badge" system. The notification and filters icon must listen for external activity triggers (e.g., new_notification, applied_filter) to display visual indicators without requiring a full page refresh.
- **Navigation Menu:** Web and mobile responsive navigation menu featuring five core modules: Home, Finances, Calendar, Messages, and Discover.
    - **Navigation Badges:** Implement a reactive "Badge" system. The navigation icons must listen for external activity triggers (e.g., unread_count, new_listing_alert) to display visual indicators without requiring a full page refresh.
- **Discover (aka Roommate Search):** Implement a Card-Stack interface supporting both Tinder-style gestures (swiping) and explicit button actions. Cards must merge User Profiles with their related Property Profile. The UI should allow for a quick toggle or "peek" into property details without leaving the discovery queue.
    - **Discover State Machine:** All profile interactions must trigger a state transition in the matchmaking lifecycle.
        - New: Default entry state; visible in the discovery pool.
        - Liked: One-way interest recorded; hidden from the sender's queue. Swipe right
        - Unliked: Soft-dismiss; removed from immediate view but potentially eligible for "Recycle" logic later. Swipe left
        - Matched: Mutual "Like" detected; triggers a message in the "Messages" module to start conversation.
        - Removed: Soft-dismiss; removed from matches but potentially eligible for "Recycle" logic later. Swipe left
        - Requested: A formal invitation sent to join a property. Swipe right
        - Accepted: Invitation confirmed; moves to the onboarding/room assignment phase. Swipe right
        - Rejected: Invitation declined; removed from matches but potentially eligible for "Recycle" logic later. Swipe left
        - Completed: Transactional finality; user is officially associated with the property in the database and assigned a room.
        - Blocked: Hard-dismiss; permanent exclusion from all interactions and visibility.
    - **Discover Ranking & Recommendation Heuristics:** Implement a weighted sorting system for the user profiles queue on the "Discover" module. Prioritize profiles using the following descending order of importance:
        - New users outside of applied filters are exlcuded from the queue (e.g. Location, Budget, Move-In Start Date, etc)
        - New users who have recently created a profile move towards the top of the queue
        - Liked users the current user are randomized to the top 50 of the queue.
        - New users who have a higher compatability score derived from similar Lifestyle, Personality and Interests attributes are moved higher in the queue
        - Unliked, removed, or rejected users are moved towards the bottom of the queue
        - Blocked users are removed from the queue forever
        - Liked, Matched, Requested, Accepted, and Completed users are hidden from the queue temporarily until Unliked, Removed, or Rejected
    - **Discover Search Filters:**
        - ____
    - **User Profile:** Allow users to effortlessly browse potential user details, and their related roommates' user details and property details. Allow for variations for viewing someone else vs yourself, property vs no proprty, roommates vs no roommates, and varying Discover matchmaking states
        - up to 6 photos
        - user-name
        - user-age
        - user-verifications (id check, credit check, background check)
        - user-occupation
        - user-company
        - user-location
        - user-max-budget
        - user-bio
        - user-lifestyle-attributes
        - user-interests-attributes-top-10
        - user-socials
        - property-pic-primary
        - property-type
        - property-bedroom-total
        - property-bathroom-total
        - property-deposit-total
        - lease-start-date
        - lease-end-date
        - user-id-roommates
    - **Property Profile:**
    - **Edit User:**
    - **Edit Property:**
- **Messaging:**
    - Connect with verified users safely.
- **Notifications**
    -  
- **Home**
- **Onboarding**
- **Settings**
    - 

---

## 🎨 Design & UI/UX

This project heavily emphasizes a clean and modern user experience. The complete design system, including typography, color palettes, and component states, was created in Figma.

- **Figma Prototype:** ____
- **Primary Colors:** `[Insert Hex Codes]`
- **Typography:** `Inter`

---

## 🛠 Tech Stack

**Client:**
- [React](https://reactjs.org/) / [Next.js](https://nextjs.org/) *(Update with your framework)*
- [React Native](https://reactnative.dev/)
- [Tailwind CSS](https://tailwindcss.com/) / [Styled Components](https://styled-components.com/) *(Update with your styling solution)*
- State Management: Context API / Redux / Zustand

**Build & Deployment:**
- Vercel

---

## 🚀 Getting Started

Follow these instructions to get a copy of the project up and running on your local machine for development and testing purposes.

### Prerequisites

Ensure you have the following installed:
- Node.js (v16.0.0 or higher)
- npm or yarn

### Installation

1. **Clone the repository:**
   ```bash
   git clone [https://github.com/yourusername/roomi-app.git](https://github.com/yourusername/roomi-app.git)
