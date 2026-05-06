What is Multi-Stage Build and Why Use It?
When we build a Node.js app, we need a ton of tools and dependencies just to compile it — but we don't need any of that to actually serve it. A multi-stage build lets us separate the building from the serving, so the final image only contains what's truly needed to run the app. Smaller image, faster deployments, less attack surface.

Why This Matters
Think of it like cooking a meal. The installer stage is your full kitchen — ingredients, utensils, prep work, the mess. The deployer stage is just the plate that goes to the table. Your guest doesn't need to see the kitchen.
Single-Stage Build Multi-Stage Build 
Image sizeLarge (includes Node, npm, source files) Small (only Nginx + build output)
Security More packages = more vulnerabilities Minimal surface area
Build tools in production❌ Present but not needed✅ Stripped out
Deploy speed  SlowerFaster

How to Build and Run
bash# Build the image
docker build -t my-app .

# Run it (maps port 80 inside container to 8080 on your machine)
docker run -p 8080:80 my-app
Then open http://localhost:8080 and your app is live — served by Nginx, with none of the build clutter included.

Recommended: Add a .dockerignore
Put this in the same folder as your Dockerfile to prevent unnecessary files from being copied into the build context:
node_modules
.git
.env
*.log
build
This keeps builds clean and fast.
