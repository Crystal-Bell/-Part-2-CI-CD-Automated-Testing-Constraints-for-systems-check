# -Part-2-CI-CD-Automated-Testing-Constraints-for-systems-check
.github/workflows/systems-check-constraints.yml:
name: "⚙️ Transdisciplinary Systems Check & Constraints"

on:
  push:
    branches: [ "master", "main" ]
  pull_request:
    branches: [ "master", "main" ]

jobs:
  validate-ecosystem-constraints:
    runs-on: ubuntu-latest

    strategy:
      matrix:
        node-version: [18.x, 20.x]

    steps:
    - name: "📥 Checkout Architecture Repository"
      uses: actions/checkout@v4

    - name: "🟢 Initialize Node.js Environment (${{ matrix.node-version }})"
      uses: actions/with-node@v4
      with:
        node-version: ${{ matrix.node-version }}
        cache: 'npm'

    - name: "📦 Install System Dependencies"
      run: npm ci

    - name: "🧬 Constraint 1: Structural Taxonomy Verification"
      run: |
        echo "Verifying structural keyword indexing maps to Master Hub constraints..."
        # Fails the build if core transdisciplinary folders or mappings are completely missing
        if [ ! -d "src/tools" ]; then
          echo "❌ CRITICAL FAULT: Agent-C capability definitions folder missing!"
          exit 1
        fi

    - name: "🤖 Constraint 2: Run Agent-C Tool Unit Tests"
      run: |
        echo "Executing unit tests for Genesis-Covenant-Protocol and MCP Schemas..."
        # Runs your test suites, ensuring tools return non-empty mock JSON values 
        npm test -- --grep "Agent-C"

    - name: "🌍 Constraint 3: Verify Friction Reduction Logic Profiles"
      run: |
        echo "Validating Madcola resource transformation equation boundaries..."
        # Runs integration tests assessing boundaries (e.g., ensuring polymer yield math doesn't return negative numbers)
        npm run test:integration -- --grep "ResourceAutonomy"

    - name: "🔒 Post-System-Check Summary"
      if: always()
      run: |
        echo "Systems Check completed with code execution state: ${{ job.status }}"
