---
name: devops-deployment
description: Deploy code to production through CI/CD pipeline. This agent is the ONLY one allowed to commit and push code.
---

# Skill: devops-deployment

## Overview
Deploy code to production through CI/CD pipeline. This agent is the ONLY one allowed to commit and push code.

## When to Use
- After code review is approved
- When new features need to go to production
- For hotfixes and urgent deployments

## The Process

### Step 1: Receive Deploy Request
Receive package from reviewer containing:
- Commit SHA or diff
- Branch name
- Review report
- Test results
- Expected version

### Step 2: Final Review
- Quick sanity check (5 min max)
- Verify tests passed
- Check for obvious issues

### Step 3: Commit & Push
- Create conventional commit message
- Commit the changes
- Push to remote branch

### Step 4: Monitor CI/CD
- Wait for Coolify build (~60 seconds)
- Monitor build logs
- Check for build failures

### Step 5: Verify Deployment
- Poll /health endpoint
- Verify version matches expected
- Confirm deployment success

### Step 6: Notify Tester
- Send DEPLOY_SUCCESS notification to @tester
- Include: version, endpoint, test tokens

## Error Handling

### Build Failure
- Check CI/CD logs
- Notify coder to fix
- Block deployment

### Deploy Timeout
- Health check not passing after 120s
- Investigate logs
- Notify team

### Version Mismatch
- Deployed version != expected
- Check pyproject.toml
- Re-deploy if needed

## Commands

```bash
# Commit and push
git add .
git commit -m "type: description"
git push origin branch

## Integration

Called by:
- Orchestrator after reviewer approval
- Manual deploy requests

Calls:
- @tester after successful deploy
