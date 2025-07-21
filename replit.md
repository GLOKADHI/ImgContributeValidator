# Stock Photo Analysis Tool

## Overview

This is a modern web application that analyzes images and videos for stock photography purposes using AI. The application allows users to upload images or videos and receive detailed analysis including descriptions, keywords, categorization, and market viability assessments. For videos, the system automatically extracts multiple frames and allows users to select the best frame for analysis. Built with a React frontend and Express backend, it leverages OpenAI's GPT-4o for intelligent image analysis.

## User Preferences

Preferred communication style: Simple, everyday language.

## System Architecture

### Frontend Architecture
- **Framework**: React 18 with TypeScript
- **Routing**: Wouter for lightweight client-side routing
- **UI Components**: Shadcn/ui component library with Radix UI primitives
- **Styling**: Tailwind CSS with CSS variables for theming
- **State Management**: TanStack Query (React Query) for server state management
- **Build Tool**: Vite for fast development and optimized builds

### Backend Architecture
- **Framework**: Express.js with TypeScript
- **Runtime**: Node.js with ES modules
- **API Design**: RESTful API endpoints
- **File Handling**: Multer for multipart form data and image uploads
- **Image Processing**: Base64 encoding for AI analysis

### Data Storage
- **Database**: PostgreSQL with Drizzle ORM
- **Database Provider**: Neon serverless PostgreSQL
- **Schema Management**: Drizzle migrations
- **Development Storage**: In-memory storage fallback for development

### Authentication & Authorization
- **Session Management**: Express sessions with PostgreSQL session store
- **Security**: Basic session-based authentication (prepared for user system)

## Key Components

### Image Analysis Service
- **AI Provider**: OpenAI GPT-4o for advanced image analysis
- **Analysis Features**: 
  - Detailed image descriptions with user-defined character limits (50-500 chars)
  - Keyword generation (configurable count 5-50)
  - Category and subcategory classification
  - Technical quality assessment including resolution analysis
  - Commercial appeal evaluation
  - Market demand analysis
  - Acceptance rate prediction based on image quality and dimensions
  - Customer review integration for personalized analysis

### Database Schema
- **Users Table**: User authentication and profile data
- **Image Analyses Table**: Stores complete analysis results including:
  - File metadata (name, size, dimensions, resolution)
  - AI-generated content (description, keywords, categories)
  - Quality metrics (technical, commercial, market assessments)
  - Customer reviews and feedback
  - Timestamps for tracking

### API Endpoints
- `POST /api/analyze`: Process image analysis requests
- `GET /api/stats`: Retrieve analysis statistics and metrics

### UI Components
- **File Upload**: Enhanced drag-and-drop interface supporting both images and videos with file validation and global paste support
- **Video Frame Extraction**: Automatic extraction of 10 frames from uploaded videos with visual frame selection grid
- **Best Frame Selection**: Interactive frame selector allowing users to choose the optimal frame for analysis
- **Metadata Display**: Resolution, megapixels, aspect ratio, and quality indicators for both images and video frames
- **Analysis Controls**: Keyword count slider (5-50), character limit slider (50-500), and customer review input
- **Results Display**: Comprehensive analysis presentation with character counters
- **Statistics Dashboard**: Usage metrics and performance indicators

## Data Flow

### Image Analysis Flow
1. **File Upload**: User selects, drags, or pastes image/video file to upload interface
2. **File Type Detection**: System determines if uploaded file is image or video
3. **Video Processing** (if video): Extract 10 frames using HTML5 video canvas API, display frame selection grid
4. **Frame Selection** (if video): User selects best frame from extracted frames grid
5. **Metadata Extraction**: Frontend extracts dimensions, calculates megapixels and quality metrics from selected frame/image
6. **File Processing**: Convert selected frame or image to base64 for API transmission
7. **API Request**: Analysis request sent to backend with image data, parameters, and optional customer review
8. **AI Analysis**: OpenAI GPT-4o processes image with resolution context and customer feedback for tailored analysis
9. **Data Storage**: Analysis results with full metadata stored in PostgreSQL database
10. **Response Delivery**: Results with character counts and quality indicators returned to frontend
11. **Statistics Update**: Analysis metrics updated for dashboard display

## Recent Changes (July 19, 2025)

### Enhanced Image Metadata Support
- Added automatic extraction of image dimensions (width × height)
- Real-time calculation of megapixels and aspect ratio
- Quality assessment based on resolution (High: 6+ MP, Medium: 3-6 MP, Low: <3 MP)
- Visual metadata display with color-coded quality indicators

### Character Limit Control
- User-configurable character limits for descriptions (50-500 characters)
- Real-time character counter with color-coded status
- AI respects character limits during analysis generation

### Customer Review Integration
- Optional customer review/feedback input field
- AI adjusts analysis based on customer feedback
- Personalized acceptance rates and quality assessments
- Enhanced prompts with customer context

### Video Upload and Frame Selection
- Full video upload support (MP4, WebM, MOV formats)
- Real-time upload progress indicator with percentage and frame counter
- Automatic video frame extraction using HTML5 Canvas API
- Extraction of 10 evenly distributed frames across video duration
- Progress tracking during frame extraction process
- Interactive frame selection grid with visual feedback
- Real-time preview updates when switching between frames
- Middle frame selected as default "best frame" for initial analysis
- File size display and processing status updates

### Technical Improvements
- Increased server payload limit to 500MB for large image and video uploads
- Enhanced drag-and-drop visual feedback with scaling effects supporting multiple file types
- Global keyboard paste support (Ctrl+V anywhere on page)
- Improved error handling for large files and video processing failures
- Client-side video processing using HTML5 video element and canvas rendering

## External Dependencies

### Core Dependencies
- **@neondatabase/serverless**: Serverless PostgreSQL client
- **drizzle-orm**: Type-safe database toolkit
- **openai**: Official OpenAI API client
- **@tanstack/react-query**: Server state management
- **@radix-ui/***: Accessible UI component primitives
- **tailwindcss**: Utility-first CSS framework

### Development Tools
- **Vite**: Build tool and dev server
- **TypeScript**: Type safety and development experience
- **ESBuild**: Fast JavaScript bundler for production
- **Drizzle Kit**: Database migration and schema management

### AI Integration
- **OpenAI API**: GPT-4o model for image analysis
- **Image Processing**: Base64 encoding for API compatibility

## Deployment Strategy

### Build Process
- **Frontend**: Vite builds optimized React bundle
- **Backend**: ESBuild compiles TypeScript server code
- **Output**: Static frontend assets and Node.js server bundle

### Environment Configuration
- **Database**: Requires `DATABASE_URL` for PostgreSQL connection
- **AI Service**: Requires `OPENAI_API_KEY` for OpenAI API access
- **Development**: Automatic Replit integration with error overlay

### Production Considerations
- **Database Migrations**: Managed through Drizzle Kit
- **Static Assets**: Served through Express in production
- **Error Handling**: Comprehensive error boundaries and API error responses
- **Performance**: Optimized builds with code splitting and lazy loading

The application follows modern full-stack patterns with clear separation of concerns, type safety throughout, and a focus on user experience and performance.