---
title: "Meshery CLI Commands for Organization, Workspaces, and Connections"
url: "https://meshery.io/blog/2025/11/2025-10-31-mesheryctl-new-cmds-org-workspace/"
date: "2025-11-03T05:00:00+00:00"
author: "Aadhitya Amarendiran"
feed_url: "https://meshery.io/feed.xml"
---
<p>Introducing new <code class="language-plaintext highlighter-rouge">mesheryctl</code> commands that enhance organization and workspace management capabilities. These commands empower users to efficiently manage their Meshery organizations and workspaces directly from the command line.</p>

<p>Whether you’re just getting started with Meshery or expanding collaboration across teams, these experimental commands bring day-to-day actions—like listing organizations, creating workspaces, and managing connections—into a consistent CLI workflow.</p>

<h3 id="what-youll-find-in-this-blog-post">What you’ll find in this blog post</h3>

<ul>
  <li>A quick primer to understand more about Organizations, Workspaces and Connections in Meshery.</li>
  <li>Step-by-step usage for each command with examples.</li>
  <li>Notes, tips, and troubleshooting guidance to avoid common pitfalls.</li>
</ul>

<p>Note on stability: All commands in this post are currently experimental. Behavior and output formats may change as the features mature.</p>

<h3 id="quick-primer-terminology">Quick primer (terminology)</h3>

<ul>
  <li>Organization: Your Meshery Cloud tenant. Users belong to one or more organizations.</li>
  <li>Workspace: A collaboration area within an organization. Use workspaces to group Designs, Environments, teams, or projects.</li>
  <li>Connection: An integration endpoint (for example, Kubernetes clusters or Meshery platforms) associated with your Meshery profile.</li>
</ul>

<h3 id="prerequisites">Prerequisites</h3>

<ul>
  <li><code class="language-plaintext highlighter-rouge">mesheryctl</code> installed and configured.</li>
  <li>Logged in to Meshery Cloud with access to at least one organization.</li>
  <li>Appropriate permissions in the target organization to list and/or create resources.</li>
</ul>

<p>Tip: If a command fails with “unauthorized” or “forbidden,” verify that you are logged in with the correct account and that your role in the organization allows the requested action.</p>

<h2 id="connection">Connection</h2>

<p><code class="language-plaintext highlighter-rouge">connection</code> command helps users to view and manage Meshery connections with respect to the user’s profile in Meshery. This command is currently in <code class="language-plaintext highlighter-rouge">experimental</code> mode. Using this command, one can view the number of connections associated with their profile in Meshery and can delete unused connections if present. To know more info about Meshery connections concept in general, please refer to <a href="https://docs.meshery.io/concepts/logical/connections">Connections in Meshery</a></p>

<h3 id="base-command-syntax">Base command syntax</h3>

<div class="language-plaintext highlighter-rouge"><div class="highlight"><pre class="highlight"><code>mesheryctl exp connections
</code></pre></div></div>

<p>Current available subcommands present are: delete and list.
delete - This subcommand is used to delete a connection in Meshery
list - List all available Meshery connections</p>

<p>Flags available:
-c,–count - To display total number of available connections</p>

<p>Examples:
For listing connections:</p>

<div class="language-plaintext highlighter-rouge"><div class="highlight"><pre class="highlight"><code>&gt; mesheryctl exp connections list
Total number of connections: 5
Page: 1
ID                                    NAME                     TYPE      KIND        STATUS
b0122ae9-...  in-cluster               platform  kubernetes  connected
467fd193-...  meshery-shocker-0        platform  meshery     connected
b481abd6-...  meshery-m.o.d.o.k.-3     platform  meshery     connected
4d51bff0-...  kubernetes-meshfusion-3  platform  kubernetes  not found
a85478df-...  meshery-sentinel-1       platform  meshery     connected
</code></pre></div></div>

<p>For deleting a connection:</p>

<div class="language-plaintext highlighter-rouge"><div class="highlight"><pre class="highlight"><code>&gt; mesheryctl exp connections delete 22xg3…
Connection deleted
</code></pre></div></div>

<h3 id="notes-and-tips">Notes and tips</h3>

<ul>
  <li>“not found” status usually indicates the target system is no longer reachable. Consider removing such connections.</li>
  <li>Deleting a connection cannot be undone. Ensure the ID is correct before deleting.</li>
  <li>If you manage multiple environments, run list regularly to keep connections tidy.</li>
</ul>

<h3 id="troubleshooting">Troubleshooting</h3>

<ul>
  <li>“resource not found”: Verify the connection ID from the latest list output.</li>
  <li>“forbidden” or “unauthorized”: Confirm your Meshery login and account permissions.</li>
</ul>

<h2 id="organization">Organization</h2>

<p><code class="language-plaintext highlighter-rouge">organization</code> command allows users to view organizations which they are part of in the Meshery Cloud. This command is in <code class="language-plaintext highlighter-rouge">experimental</code> mode and users can currently view the organizations they are in as a member.</p>

<h3 id="base-syntax">Base syntax</h3>

<div class="language-plaintext highlighter-rouge"><div class="highlight"><pre class="highlight"><code>mesheryctl exp organization
</code></pre></div></div>

<h3 id="available-subcommands">Available subcommands</h3>

<p>list - List all organizations that user is part of in Meshery Cloud</p>

<p>Example:</p>

<div class="language-plaintext highlighter-rouge"><div class="highlight"><pre class="highlight"><code>&gt; mesheryctl exp organization list
Total number of organizations:2
Page: 1
NAME      ID                  CREATED-AT
Meshery   c5ada327-...    2025/September/10
XYZ   ce8a571e-...    2024/August/19
</code></pre></div></div>

<h3 id="notes-and-tips-1">Notes and tips</h3>

<ul>
  <li>If you expect to see an organization but don’t, ask an admin to confirm your membership.</li>
  <li>Use the organization ID from this list when creating or listing workspaces.</li>
</ul>

<h3 id="troubleshooting-1">Troubleshooting</h3>

<ul>
  <li>“no organizations found”: Confirm that your Meshery account is connected to Meshery Cloud and that you’ve been invited to an organization.</li>
</ul>

<h2 id="workspaces">Workspaces</h2>

<p><code class="language-plaintext highlighter-rouge">workspace</code> command allows users to create workspaces within an organization which can act as a hub for teams to work and collaborate in Meshery. Workspaces are useful to organize project-based work or to create domains of responsibility for your teams or segregate Designs and Environments and track team activity.</p>

<p>Currently, this command is in <code class="language-plaintext highlighter-rouge">experimental</code> mode and users can create workspaces in the organisation they are in, list workspaces present. For more info about workspaces in Meshery, please refer to <a href="https://docs.meshery.io/concepts/logical/workspaces">Workspaces in Meshery</a>.</p>

<h3 id="base-command">Base command</h3>

<div class="language-plaintext highlighter-rouge"><div class="highlight"><pre class="highlight"><code>mesheryctl exp workspace
</code></pre></div></div>

<p>Available subcommands:
create - Create a workspace within an organization in Meshery
list - List all available workspaces present within an organization in Meshery</p>

<p>Example:
To list workspaces in an organization:</p>

<div class="language-plaintext highlighter-rouge"><div class="highlight"><pre class="highlight"><code>&gt; mesheryctl exp workspace list --orgId ce8ffxe-...
Total number of workspaces:3
Page: 1
ID                                    NAME        DESCRIPTION
9a21b6e1-...  platform-team  Platform engineering workspace
b77c19f9-...  test-1         Test workspace
c05a3c3a-...  staging        Staging experiments
</code></pre></div></div>

<p>To create a workspace in an organization:</p>

<div class="language-plaintext highlighter-rouge"><div class="highlight"><pre class="highlight"><code>&gt; mesheryctl exp workspace create --orgId ce8ffxe-... --name test-1 --desc "Test workspace"
Workspace created: test-1
</code></pre></div></div>

<h3 id="notes-and-tips-2">Notes and tips</h3>

<ul>
  <li>Workspace names should be clear to your team (for example, “platform-team” or “payments-observability”).</li>
  <li>Use the organization ID from the Organization section to scope workspace operations.</li>
  <li>If creation fails, confirm you have permissions to create resources in the target organization.</li>
</ul>

<h3 id="troubleshooting-2">Troubleshooting</h3>

<ul>
  <li>“invalid orgId”: Copy the ID exactly as shown in organization list output.</li>
  <li>“workspace already exists”: Choose a unique name or delete the existing workspace if appropriate.</li>
</ul>

<p>NOTE: These commands are evolving. Share feedback, report issues, and help improve the experience so teams can collaborate more effectively in Meshery.</p>
