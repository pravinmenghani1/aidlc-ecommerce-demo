# aidlc-ecommerce-demo

# 1. Create project directory
  mkdir aidlc-ecommerce-demo && cd aidlc-ecommerce-demo
  git init
  
  # 2. Download and install AI-DLC rules from your repo
  curl -sL https://api.github.com/repos/pravinmenghani1/aidlc-workflows/releases/latest \
    | grep -o '"browser_download_url": *"[^"]*"' \
    | head -1 | cut -d'"' -f4 \
    | xargs -I {} curl -sL {} -o /tmp/aidlc.zip

    
  unzip -o /tmp/aidlc.zip -d /tmp/aidlc-release
  
  # 3. Set up for Kiro
  mkdir -p .kiro/steering
  cp -R /tmp/aidlc-release/aidlc-rules/aws-aidlc-rules .kiro/steering/

  
  cp -R /tmp/aidlc-release/aidlc-rules/aws-aidlc-rule-details .kiro/

  
  rm -rf /tmp/aidlc.zip /tmp/aidlc-release
  
  # 4. Verify: run kiro-cli, then /context show
  # Confirm entries for .kiro/steering/aws-aidlc-rules
