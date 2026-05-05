---
title: "Meshery Workspaces"
url: "https://meshery.io/blog/2026/02/2026-02-16-meshery-workspaces-enabling-cross-team-collaboration/"
date: "2026-02-16T16:00:00+00:00"
author: "Meshery Team"
feed_url: "https://meshery.io/feed.xml"
---
<p>In modern cloud-native environments, platform engineering teams face a persistent challenge: how do you enable multiple teams to collaborate on infrastructure designs, share best practices, and maintain consistency across diverse deployment environments—all while preserving team autonomy and security boundaries?</p>

<p>Enter <strong>Meshery Workspaces</strong>: a powerful organizational construct designed to facilitate exactly this kind of cross-team collaboration. Workspaces provide isolated, multi-tenant environments where teams can design, test, and share cloud-native infrastructure patterns without stepping on each other’s toes.</p>

<h2 id="what-are-meshery-workspaces">What Are Meshery Workspaces?</h2>

<p>At their core, <a href="https://docs.meshery.io/concepts/logical/workspaces">Workspaces</a> are logical boundaries within Meshery that allow you to organize your infrastructure designs, deployments, and environments. Think of them as collaborative project spaces where:</p>

<ul>
  <li><strong>Teams maintain separate environments</strong> for development, staging, and production</li>
  <li><strong>Designs and configurations are scoped</strong> to specific organizational units or projects</li>
  <li><strong>Access controls ensure</strong> that only authorized team members can view or modify resources</li>
  <li><strong>Shared catalog items</strong> can be imported and customized without affecting the source</li>
</ul>

<p>Each Workspace operates as an independent namespace, complete with its own set of:</p>
<ul>
  <li><strong>Designs</strong>: Visual topology configurations for your infrastructure</li>
  <li><strong>Environments</strong>: Kubernetes clusters and cloud provider connections</li>
  <li><strong>Credentials</strong>: Securely stored access tokens and keys</li>
  <li><strong>Team members</strong>: Role-based access control for collaborators</li>
</ul>

<h2 id="why-platform-engineers-love-workspaces">Why Platform Engineers Love Workspaces</h2>

<p>Platform engineering is fundamentally about creating self-service capabilities that empower development teams while maintaining organizational standards. Workspaces excel at this by providing:</p>

<h3 id="1-isolation-with-collaboration">1. <strong>Isolation with Collaboration</strong></h3>
<p>Workspaces give each team their own sandbox to experiment and iterate, while still allowing platform engineers to share golden paths and reference architectures across the organization.</p>

<div class="language-plaintext highlighter-rouge"><div class="highlight"><pre class="highlight"><code>Organization
├── Platform Team Workspace
│   ├── Reference architectures
│   ├── Approved patterns
│   └── Baseline configurations
├── Backend Team Workspace
│   ├── Microservices infrastructure
│   └── API gateway configurations
└── Data Team Workspace
    ├── Data pipeline designs
    └── Analytics infrastructure
</code></pre></div></div>

<h3 id="2-design-reusability">2. <strong>Design Reusability</strong></h3>
<p>Rather than reinventing the wheel, teams can clone proven designs from Meshery’s <a href="https://meshery.io/catalog">public Catalog</a> or from other internal Workspaces. This accelerates development while ensuring consistency with organizational standards.</p>

<h3 id="3-environment-management">3. <strong>Environment Management</strong></h3>
<p>Platform engineers can configure multiple Kubernetes clusters and cloud environments within a Workspace, making it trivial to promote designs from dev to staging to production with confidence.</p>

<h3 id="4-audit-and-compliance">4. <strong>Audit and Compliance</strong></h3>
<p>Every action within a Workspace is tracked, providing clear visibility into who made what changes and when. This audit trail is invaluable for compliance and troubleshooting.</p>

<h2 id="real-world-example-multi-team-microservices-platform">Real-World Example: Multi-Team Microservices Platform</h2>

<p>Let’s walk through a practical scenario. Imagine you’re a platform engineer at a company building a microservices platform. You have:</p>
<ul>
  <li>A <strong>Platform Team</strong> maintaining infrastructure standards</li>
  <li>Multiple <strong>application teams</strong> deploying microservices</li>
  <li>A <strong>security team</strong> enforcing policies</li>
</ul>

<p>Here’s how you’d leverage Workspaces:</p>

<h3 id="step-1-create-the-golden-path-workspace">Step 1: Create the Golden Path Workspace</h3>
<p>The Platform Team creates a Workspace containing reference architectures:</p>
<ul>
  <li>Service mesh baseline (Istio with mTLS enabled)</li>
  <li>Observability stack (Prometheus, Grafana, Jaeger)</li>
  <li>Ingress patterns with rate limiting</li>
  <li>Database operator configurations</li>
</ul>

<p>These designs are marked as “approved” and published to your organization’s internal catalog section.</p>

<h3 id="step-2-application-teams-clone-and-customize">Step 2: Application Teams Clone and Customize</h3>
<p>The Backend Team needs to deploy a new microservice. Instead of starting from scratch:</p>

<ol>
  <li>They navigate to the <a href="https://meshery.io/catalog">Meshery Catalog</a></li>
  <li>Find the “Service Mesh Baseline” design from the Platform Team’s published patterns</li>
  <li>Click <strong>“Clone to Workspace”</strong></li>
  <li>The design appears in their Workspace, ready for customization</li>
</ol>

<p>Now they can:</p>
<ul>
  <li>Adjust resource limits for their specific workload</li>
  <li>Add application-specific sidecars</li>
  <li>Configure custom routing rules</li>
  <li>Deploy to their dev environment for testing</li>
</ul>

<h3 id="step-3-iterate-with-confidence">Step 3: Iterate with Confidence</h3>
<p>As the Backend Team refines their design:</p>
<ul>
  <li>Changes are isolated to their Workspace</li>
  <li>They can validate configurations against Kubernetes and OPA policies</li>
  <li>The visual designer shows real-time topology updates</li>
  <li>Once tested, they promote to staging and production environments</li>
</ul>

<h3 id="step-4-share-back-to-the-organization">Step 4: Share Back to the Organization</h3>
<p>After proving their pattern works, the Backend Team can publish their customized design back to the internal catalog with a description like “High-Throughput API Service Pattern.” Now other teams benefit from their learnings.</p>

<h2 id="workspace-features-that-drive-adoption">Workspace Features That Drive Adoption</h2>

<h3 id="visual-design-collaboration">Visual Design Collaboration</h3>
<p>Meshery’s <a href="https://docs.meshery.io/concepts/logical/designs">visual designer</a> is Workspace-aware, meaning multiple team members can collaborate on the same infrastructure design in real-time, similar to Figma for infrastructure-as-code.</p>

<h3 id="environment-promotion">Environment Promotion</h3>
<p>Workspaces support <a href="https://docs.meshery.io/concepts/logical/environments">multi-environment workflows</a>, allowing you to:</p>
<ul>
  <li>Test designs in a sandbox cluster</li>
  <li>Validate in staging with production-like data</li>
  <li>Deploy to production with a single click (with appropriate RBAC checks)</li>
</ul>

<h3 id="team-management">Team Management</h3>
<p>Fine-grained <a href="https://docs.meshery.io/concepts/logical/teams">role-based access control</a> ensures:</p>
<ul>
  <li><strong>Owners</strong> can manage Workspace settings and membership</li>
  <li><strong>Editors</strong> can modify designs and environments</li>
  <li><strong>Viewers</strong> can browse designs without making changes</li>
</ul>

<h3 id="integration-with-gitops">Integration with GitOps</h3>
<p>Workspaces integrate seamlessly with GitOps workflows:</p>
<ul>
  <li>Export designs as Kubernetes manifests or Helm charts</li>
  <li>Commit to your Git repository</li>
  <li>Let your CI/CD pipeline apply changes</li>
  <li>Meshery tracks drift between desired and actual state</li>
</ul>

<h2 id="try-it-yourself-clone-a-design-from-the-catalog">Try It Yourself: Clone a Design from the Catalog</h2>

<p>Ready to experience the power of Workspaces? Here’s a hands-on challenge:</p>

<ol>
  <li><strong>Sign up for Meshery Cloud</strong> (free tier available) or <a href="https://docs.meshery.io/installation">install Meshery locally</a></li>
  <li><strong>Navigate to the Catalog</strong> at <a href="https://meshery.io/catalog">meshery.io/catalog</a></li>
  <li><strong>Find a design that interests you</strong>, such as:
    <ul>
      <li><a href="https://meshery.io/catalog?search=observability">Kubernetes Observability Stack</a></li>
      <li><a href="https://meshery.io/catalog?search=istio">Istio Service Mesh Deployment</a></li>
      <li><a href="https://meshery.io/catalog?search=nginx">NGINX Ingress with Rate Limiting</a></li>
    </ul>
  </li>
  <li><strong>Click “Clone to Workspace”</strong> - this imports the design into your personal Workspace</li>
  <li><strong>Open the Visual Designer</strong> and explore the topology:
    <ul>
      <li>See how components are connected</li>
      <li>Adjust configurations to match your environment</li>
      <li>Add or remove resources as needed</li>
    </ul>
  </li>
  <li><strong>Connect your Kubernetes cluster</strong> (if you haven’t already)</li>
  <li><strong>Deploy the design</strong> to your environment with a single click</li>
  <li><strong>Monitor the deployment</strong> through Meshery’s built-in observability features</li>
</ol>

<p>Within minutes, you’ll have a production-ready infrastructure pattern running in your cluster, customized to your needs. That’s the power of Workspaces and the Catalog working together.</p>

<h2 id="best-practices-for-workspace-organization">Best Practices for Workspace Organization</h2>

<p>Based on patterns we’ve seen from successful platform engineering teams:</p>

<h3 id="structure-by-team-and-environment">Structure by Team and Environment</h3>
<div class="language-plaintext highlighter-rouge"><div class="highlight"><pre class="highlight"><code>├── platform-team-workspace
│   ├── Environment: prod-cluster
│   ├── Environment: staging-cluster
│   └── Designs: Reference architectures
├── backend-team-dev-workspace
│   ├── Environment: dev-cluster-1
│   └── Designs: Experimental features
└── backend-team-prod-workspace
    ├── Environment: prod-cluster
    └── Designs: Production deployments
</code></pre></div></div>

<h3 id="establish-naming-conventions">Establish Naming Conventions</h3>
<ul>
  <li>Workspaces: <code class="language-plaintext highlighter-rouge">&lt;team&gt;-&lt;environment&gt;-workspace</code></li>
  <li>Designs: <code class="language-plaintext highlighter-rouge">&lt;service&gt;-&lt;version&gt;-&lt;purpose&gt;</code></li>
  <li>Environments: <code class="language-plaintext highlighter-rouge">&lt;cluster-name&gt;-&lt;region&gt;</code></li>
</ul>

<h3 id="implement-a-promotion-workflow">Implement a Promotion Workflow</h3>
<ol>
  <li>Develop and test in team dev Workspace</li>
  <li>Promote stable designs to team staging Workspace</li>
  <li>After validation, promote to team prod Workspace</li>
  <li>Share successful patterns to organization-wide Workspace</li>
</ol>

<h3 id="leverage-teams-and-rbac">Leverage Teams and RBAC</h3>
<ul>
  <li>Create Teams that span multiple Workspaces</li>
  <li>Grant minimum necessary permissions</li>
  <li>Use Viewer role for cross-team visibility</li>
  <li>Reserve Owner role for platform engineers</li>
</ul>

<h2 id="the-future-of-collaborative-infrastructure">The Future of Collaborative Infrastructure</h2>

<p>Meshery Workspaces represent a fundamental shift in how platform engineering teams approach infrastructure management. By combining:</p>
<ul>
  <li><strong>Visual design</strong> tools that make complex topologies understandable</li>
  <li><strong>Collaborative features</strong> that break down silos</li>
  <li><strong>Reusable patterns</strong> through the Catalog</li>
  <li><strong>Strong isolation</strong> with flexible sharing</li>
</ul>

<p>Workspaces empower organizations to move faster without sacrificing control. They enable the kind of self-service infrastructure that development teams crave, while giving platform engineers the governance capabilities they need.</p>

<h2 id="get-started-today">Get Started Today</h2>

<p>Whether you’re managing infrastructure for a small startup or orchestrating deployments across a large enterprise, Meshery Workspaces can transform how your teams collaborate.</p>

<p><strong>Start your journey:</strong></p>
<ul>
  <li>📚 <a href="https://docs.meshery.io/concepts/logical/workspaces">Read the Workspaces documentation</a></li>
  <li>🎨 <a href="https://docs.meshery.io/concepts/logical/designs">Explore the Visual Designer</a></li>
  <li>📦 <a href="https://meshery.io/catalog">Browse the Catalog</a></li>
  <li>🚀 <a href="https://docs.meshery.io/installation">Install Meshery</a></li>
</ul>

<p><strong>Join the community:</strong></p>
<ul>
  <li>💬 <a href="http://slack.meshery.io">Slack</a></li>
  <li>🐙 <a href="https://github.com/meshery/meshery">GitHub</a></li>
  <li>🐦 <a href="https://twitter.com/mesheryio">Twitter</a></li>
</ul>

<p>Clone a design, customize it in your Workspace, and deploy it to your cluster today. Experience firsthand how Workspaces can accelerate your platform engineering efforts while maintaining the control and visibility your organization demands.</p>

<hr />

<p><em>Have questions about Workspaces or want to share your use case? Join us in the <a href="https://slack.meshery.io">Meshery community</a> - we’d love to hear from you!</em></p>
