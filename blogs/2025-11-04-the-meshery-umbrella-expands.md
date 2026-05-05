---
title: "The Meshery Umbrella Expands"
url: "https://meshery.io/blog/2025/meshery-ecosystem-expansion"
date: "2025-11-04T18:00:00+00:00"
author: "Lee Calcote, Sangram Rath, Matthieu Evrin, Mia Grenell"
feed_url: "https://meshery.io/feed.xml"
---
<p>Meshery’s <a href="https://meshery.io/blog/sixth-highest-velocity-cncf-project">high project velocity</a> necessitates a revision in its governance and organizational structure to align with the scale of its growing complexity and community contributions. To best serve its expansive ecosystem, Meshery maintainers have opted to partition its numerous GitHub repositories into two distinct organizations: <a href="https://github.com/meshery">Meshery</a> for the core platform and <a href="https://github.com/meshery-extensions">Meshery Extensions</a> for <a href="https://meshery.io/extensions">extensions</a>.</p>

<p>This strategic move aims to enhance the project’s structure, manageability, scalability, and community engagement. This post outlines the rationale, suggested governance structure, support expectations, and project mechanics behind this decision, drawing parallels with similar strategies employed by other graduated projects.</p>

<h2 id="rationale-for-repository-partitioning">Rationale for Repository Partitioning</h2>

<p>The decision to split Meshery’s repositories into two GitHub organizations is driven by several strategic considerations.</p>

<h3 id="project-architecture">Project Architecture</h3>

<p>Meshery’s architectural project structure is that of a highly extensible, self-service, management platform. With every feature developed, rigorous consideration is given to extensibility as is evident by the ubiquity of <a href="https://docs.meshery.io/extensibility#extension-points">extension points</a> throughout Meshery’s architecture.</p>

<h3 id="modularity-and-focus">Modularity and Focus</h3>

<p>Separating the core platform from extensions allows the Meshery core team to concentrate on maintaining and enhancing the primary platform, which includes critical components like Meshery Operator and MeshSync. Extensions, such as adapters for specific cloud native technologies, can be developed and maintained independently by community contributors or specialized teams. This modularity ensures that the core platform remains robust and focused.</p>

<h3 id="project-scalability">Project Scalability</h3>

<p>As Meshery supports over 300 integrations and continues to grow, the number of extensions is expected to increase. Managing these within a single organization could become unwieldy. A separate organization for extensions simplifies permission management, contribution processes, and release cycles, making the ecosystem more scalable.</p>

<ul>
  <li><strong>Community Ownership and Maintenance:</strong> Projects within <code class="language-plaintext highlighter-rouge">meshery-extensions</code> are generally initiated, developed, and maintained by members of the wider Meshery community, rather than the core Meshery maintainers. This allows the ecosystem to scale beyond what the core team can directly support.</li>
  <li><strong>Clearer Support Expectations:</strong> Separating community contributions makes it clearer that projects in <code class="language-plaintext highlighter-rouge">meshery-extensions</code> might have different maintenance levels, release cadences, and support guarantees compared to the core Meshery components. Users understand they are relying on community support for these specific integrations.</li>
</ul>

<h3 id="community-engagement">Community Engagement</h3>

<p>By providing a dedicated space for extensions, Meshery encourages community contributions. Developers can create and maintain extensions without needing deep involvement in the core platform’s development, fostering a vibrant ecosystem. This approach aligns with Meshery’s emphasis on collaborative design and operation, as highlighted in its documentation (Meshery Overview). In essence, <code class="language-plaintext highlighter-rouge">meshery-extensions</code> fosters a vibrant ecosystem around Meshery by providing a designated, community-centric space for extensions, integrations, and tooling, keeping the core project focused and manageable while enabling broad community participation.</p>

<ul>
  <li><strong>Incubation and Experimentation:</strong> The separate organization acts as an incubator for new ideas, providers, or tooling related to Meshery. Projects might start here and, if they gain significant traction and stability, could potentially be considered for migration or closer integration with the core project.</li>
  <li><strong>Ecosystem Growth:</strong> Part of Meshery’s power lies in its ability to manage <em>any</em> infrastructure via Providers, <a href="https://docs.meshery.io/concepts/logical/models">Models</a>, Adapters, and its other extension points. Since there are countless APIs and services, <code class="language-plaintext highlighter-rouge">meshery-extensions</code> serves as the place for the community to build and share Providers for less common cloud services, specific SaaS platforms, or even internal company APIs, without needing official endorsement or maintenance from the core maintainers.</li>
</ul>

<h2 id="governance-structure">Governance Structure</h2>

<p>This expansion allows for different governance models or maintainer structures for community projects compared to the core project. To effectively manage the two organizations, Meshery can adopt a governance model that balances control over the core platform with flexibility for extensions, drawing from its existing governance (Meshery Governance) and Kubernetes’ SIG model.</p>

<h3 id="core-platform-githubcommeshery">Core Platform (<a href="https://github.com/meshery">github.com/meshery</a>)</h3>

<ul>
  <li><strong>Governance</strong>: Governed by the core Meshery maintainers, as outlined in the project’s governance document. Roles include contributors, organization members, and maintainers, with clear processes for becoming a maintainer (e.g., nomination, voting by existing maintainers).</li>
  <li><strong>Responsibilities</strong>: Maintainers review, approve, and merge pull requests, manage releases, and ensure the platform’s stability and alignment with CNCF standards.</li>
  <li><strong>Decision-Making</strong>: Decisions are made through consensus among maintainers, with regular meetings and transparent communication via Slack and community forums.</li>
</ul>

<h3 id="extensions-githubcommeshery-extensions">Extensions (<a href="https://github.com/meshery-extensions">github.com/meshery-extensions</a>)</h3>

<ul>
  <li><strong>Governance</strong>: Each extension may have its own maintainers, potentially with a lighter governance structure to encourage innovation. A review process by the core team ensures extensions meet quality and compatibility standards.</li>
  <li><strong>Maintainer Selection</strong>: Extension maintainers can be nominated by community members or self-nominated, with approval from the core team based on contribution history and technical expertise.</li>
  <li><strong>Autonomy</strong>: Extension teams have autonomy over their development processes, provided they adhere to Meshery’s code of conduct and integration guidelines.</li>
</ul>

<h3 id="oversight-and-coordination">Oversight and Coordination</h3>

<ul>
  <li><strong>Steering Committee</strong>: A steering committee, comprising core maintainers and representatives from active extension teams, oversee cross-organization alignment, resolve conflicts, and approve new extensions.</li>
  <li><strong>Transparency</strong>: Both organizations maintain open communication with public meeting minutes, discussion forums, and regular updates to the community.</li>
</ul>

<table>
  <thead>
    <tr>
      <th>Aspect</th>
      <th>Core Platform</th>
      <th>Extensions</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td><strong>Governance</strong></td>
      <td>Structured, led by core maintainers</td>
      <td>Flexible, per-extension maintainers</td>
    </tr>
    <tr>
      <td><strong>Maintainer Selection</strong></td>
      <td>Nomination, 2/3rds majority vote</td>
      <td>Nomination, core team approval</td>
    </tr>
    <tr>
      <td><strong>Decision-Making</strong></td>
      <td>Consensus among maintainers</td>
      <td>Extension team consensus, core oversight</td>
    </tr>
    <tr>
      <td><strong>Communication</strong></td>
      <td>Public meetings, Slack, forums</td>
      <td>Public issues, Slack, optional meetings</td>
    </tr>
  </tbody>
</table>

<h2 id="delineated-support-expectations">Delineated Support Expectations</h2>

<p>Support expectations differ between the core platform and extensions to reflect their distinct roles and maintenance models.</p>

<h3 id="core-platform">Core Platform</h3>

<ul>
  <li><strong>Full Support</strong>: The core team provides regular updates, bug fixes, and feature enhancements, ensuring stability for critical components like Meshery Operator and MeshSync.</li>
  <li><strong>Documentation</strong>: Comprehensive guides, such as installation instructions and CLI usage, are maintained (Meshery Documentation).</li>
  <li><strong>Community Support</strong>: Active engagement through Slack, forums, and weekly newcomer meetings supports users and contributors.</li>
</ul>

<h3 id="extensions">Extensions</h3>

<ul>
  <li><strong>Variable Support</strong>: Support depends on the extension’s maintainers. Core team-maintained extensions (e.g., Istio adapter) receive robust support, while community-maintained ones may have limited support.</li>
  <li><strong>Clear Labeling</strong>: Documentation should indicate the support level (e.g., “Official” vs. “Community”) for each extension to set user expectations.</li>
  <li><strong>Integration Support</strong>: The core platform provides stable APIs and extension points, ensuring compatibility, with guidelines for developers (Meshery Extensions).</li>
</ul>

<h3 id="user-guidance">User Guidance</h3>

<ul>
  <li><strong>Documentation</strong>: Both core and extension documentation should be accessible, with clear instructions on installation, usage, and troubleshooting.</li>
  <li><strong>Community Channels</strong>: Users can seek help via <a href="https://slack.meshery.io">Slack</a>, GitHub issues, or the <a href="https://meshery.io/community#discussion-forums">discussion forum</a>.</li>
</ul>

<h2 id="project-mechanics">Project Mechanics</h2>

<p>The mechanics of managing two organizations involve distinct development, testing, and integration processes to ensure a cohesive ecosystem.Development Process</p>

<ul>
  <li><strong>Platform</strong>: Follows a structured release cycle with <a href="https://docs.meshery.io/project/contributing/build-and-release">stable and edge channels</a>. Changes undergo rigorous review to maintain stability. Notify platform extenders and system integrators of upcoming changes in the underlying framework to ensure time is afforded to maintain compatibility.</li>
  <li><strong>Extensions</strong>: Operate on independent release cycles, allowing rapid iteration. Developers use Meshery’s extension points to integrate with the core platform, following <a href="https://docs.meshery.io/project/contributing">contribution guidelines</a>.</li>
</ul>

<h3 id="integration-testing">Integration Testing</h3>

<ul>
  <li><strong>Compatibility Testing</strong>: Extensions are tested against multiple core platform versions to ensure compatibility, using guidance for <a href="https://docs.meshery.io/extensibility/verify-compatibility">verifying compatibility</a> between core platform and extensions.</li>
  <li><strong>Automated Pipelines</strong>: GitHub Actions automate testing and snapshot generation, as seen in extensions like <a href="https://meshery.io/extensions/helm-kanvas-snapshot">Helm Kanvas Snapshot</a>.</li>
  <li><strong>Performance Testing</strong>: Meshery’s performance management features can be used to benchmark extensions, ensuring they meet efficiency standards.</li>
</ul>

<h3 id="documentation-and-onboarding">Documentation and Onboarding</h3>

<ul>
  <li><strong>Comprehensive Guides</strong>: Documentation covers core platform usage, extension development, and integration (<a href="https://docs.meshery.io">Meshery Docs</a>). The Newcomers’ Guide and MeshMates program aid onboarding (<a href="https://meshery.io/community">Meshery Community</a>).</li>
  <li><strong>Catalog and Templates</strong>: Meshery’s catalog of design templates includes extension configurations, promoting best practices (<a href="https://meshery.io/catalog">See Meshery Catalog</a>).</li>
  <li><strong>Community Resources</strong>: Weekly meetings, Slack channels, and the <a href="https://docs.meshery.io/community/handbook">community handbook</a> provide ongoing support.</li>
</ul>

<h2 id="reflections-on-other-projects">Reflections on Other Projects</h2>

<p>Meshery’s expansion strategy draws inspiration from successful models within the Cloud Native Computing Foundation (CNCF), like Argo, Crossplane, and Kubernetes. These projects demonstrate effective approaches to decentralized governance and focused development through the separation of core and community-contributed components.</p>

<p>Meshery aims to emulate Crossplane’s model of maintaining a clear distinction between its core platform (<a href="https://github.com/crossplane">github.com/crossplane</a>) and community contributions (<a href="https://github.com/crossplane-contrib">github.com/crossplane-contrib</a>). This separation allows third-party developers to extend Crossplane’s capabilities without affecting the core’s stability, a model that supports Meshery’s approach to fostering innovation while maintaining a reliable core.</p>

<p>Similarly, Meshery Extension teams operate with autonomy over their development processes, provided they adhere to Meshery’s core component frameworks and integration guidelines. This mirrors Argo’s model (<a href="https://github.com/argoproj-labs">github.com/argoproj-labs</a>), where projects function independently but align with broader project goals.</p>

<p>Kubernetes provides a robust model for decentralized governance through its use of <a href="https://github.com/kubernetes">github.com/kubernetes</a> for core components and <a href="https://github.com/kubernetes-sigs">github.com/kubernetes-sigs</a> for Special Interest Groups (SIGs). Each SIG acts as a mini-community with its own charter, leadership, and processes, all while aligning with overarching project goals, as outlined in the <a href="https://github.com/kubernetes/community/blob/master/governance.md">Kubernetes Governance</a>. Meshery’s extension organization can adopt a similar structure, enabling extension teams to operate autonomously within defined guidelines.</p>

<h2 id="meshery-umbrella-expands">Meshery Umbrella Expands</h2>

<p>See the current list of repositories under each organization: <a href="https://github.com/orgs/meshery/repositories">meshery org repos</a> and <a href="https://github.com/orgs/meshery-extensions/repositories">meshery-extensions org repos</a>.</p>

<p>Meshery’s partitioning of repositories into <a href="https://github.com/meshery">github.com/meshery</a> and <a href="https://github.com/meshery-extensions">github.com/meshery-extensions</a> is a strategic move to enhance modularity, scalability, and community engagement. By adopting a governance structure that balances control and flexibility, delineating clear support expectations, and implementing robust project mechanics, Meshery can effectively manage its growing ecosystem. Drawing inspiration from graduated projects, this approach positions Meshery to remain a leading CNCF project, empowering collaborative cloud native management.</p>
