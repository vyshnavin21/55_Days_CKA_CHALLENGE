<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Kubernetes Networking — Interview Notes</title>
<style>
  * { box-sizing: border-box; margin: 0; padding: 0; }
  body {
    font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', sans-serif;
    background: #f9fafb;
    color: #1a1a2e;
    font-size: 15px;
    line-height: 1.7;
  }
  .page { max-width: 820px; margin: 0 auto; padding: 2.5rem 2rem 5rem; }
  .page-title { font-size: 1.7rem; font-weight: 700; color: #1a1a2e; margin-bottom: 4px; }
  .page-sub { font-size: 14px; color: #6b7280; margin-bottom: 2.5rem; padding-bottom: 1.5rem; border-bottom: 2px solid #e5e7eb; }
  .section { margin-bottom: 2.5rem; }
  h2 { font-size: 1.05rem; font-weight: 700; color: #1a1a2e; margin-bottom: 0.75rem; display: flex; align-items: center; gap: 8px; }
  h2 .num { width: 22px; height: 22px; background: #1a1a2e; color: white; border-radius: 50%; font-size: 11px; font-weight: 700; display: inline-flex; align-items: center; justify-content: center; flex-shrink: 0; }
  p { margin-bottom: 0.5rem; color: #374151; font-size: 14.5px; }
  p:last-child { margin-bottom: 0; }
  .card { background: white; border: 1px solid #e5e7eb; border-radius: 10px; padding: 1.1rem 1.25rem; margin-bottom: 0.75rem; }
  .card-label { font-size: 11px; font-weight: 700; text-transform: uppercase; letter-spacing: 0.08em; color: #9ca3af; margin-bottom: 0.5rem; }
  .grid2 { display: grid; grid-template-columns: 1fr 1fr; gap: 0.75rem; }
  code { font-family: 'SFMono-Regular', Consolas, monospace; font-size: 12px; background: #f3f4f6; color: #374151; padding: 1px 5px; border-radius: 4px; }
  .code-block { background: #1e2636; color: #cdd9e5; border-radius: 8px; padding: 0.9rem 1.1rem; font-family: 'SFMono-Regular', Consolas, monospace; font-size: 12.5px; line-height: 1.75; margin: 0.5rem 0; overflow-x: auto; }
  .hl-green { color: #56d364; }
  .hl-blue  { color: #79c0ff; }
  .hl-amber { color: #e3b341; }
  .hl-muted { color: #6e7681; }
  .flow { display: flex; align-items: center; flex-wrap: wrap; gap: 6px; font-family: 'SFMono-Regular', Consolas, monospace; font-size: 12px; margin: 0.5rem 0; }
  .fn { background: #f3f4f6; border: 1px solid #d1d5db; border-radius: 6px; padding: 3px 10px; color: #374151; white-space: nowrap; }
  .fn.b { background: #eff6ff; border-color: #bfdbfe; color: #1d4ed8; }
  .fn.g { background: #f0fdf4; border-color: #bbf7d0; color: #15803d; }
  .fn.a { background: #fffbeb; border-color: #fde68a; color: #92400e; }
  .fn.t { background: #f0fdfa; border-color: #99f6e4; color: #0f766e; }
  .fa { color: #9ca3af; font-size: 13px; }
  .tag { display: inline-block; font-size: 11px; font-weight: 600; padding: 2px 9px; border-radius: 20px; margin-right: 4px; }
  .tag-blue   { background: #eff6ff; color: #1d4ed8; }
  .tag-green  { background: #f0fdf4; color: #15803d; }
  .tag-amber  { background: #fffbeb; color: #92400e; }
  .tag-teal   { background: #f0fdfa; color: #0f766e; }
  .tag-purple { background: #faf5ff; color: #6d28d9; }
  table { width: 100%; border-collapse: collapse; font-size: 13.5px; }
  th { background: #f9fafb; color: #6b7280; font-size: 11px; text-transform: uppercase; letter-spacing: 0.07em; font-weight: 700; padding: 8px 12px; text-align: left; border-bottom: 1px solid #e5e7eb; }
  td { padding: 9px 12px; border-bottom: 1px solid #f3f4f6; color: #374151; vertical-align: top; line-height: 1.5; }
  tr:last-child td { border-bottom: none; }
  td.mono { font-family: 'SFMono-Regular', Consolas, monospace; font-size: 12px; color: #1d4ed8; font-weight: 600; white-space: nowrap; }
  .callout { border-radius: 8px; padding: 1rem 1.25rem; margin: 0.75rem 0; font-size: 14px; }
  .callout-label { font-size: 11px; font-weight: 700; text-transform: uppercase; letter-spacing: 0.08em; margin-bottom: 6px; }
  .callout-warn  { background: #fffbeb; border-left: 3px solid #f59e0b; }
  .callout-warn .callout-label { color: #92400e; }
  .callout-info  { background: #eff6ff; border-left: 3px solid #3b82f6; }
  .callout-info .callout-label { color: #1d4ed8; }
  .callout-green { background: #f0fdf4; border-left: 3px solid #22c55e; }
  .callout-green .callout-label { color: #15803d; }
  .callout-purple { background: #faf5ff; border-left: 3px solid #8b5cf6; }
  .callout-purple .callout-label { color: #6d28d9; }
  .pc { display: flex; gap: 6px; font-size: 13.5px; color: #374151; margin: 3px 0; }
  .pro { color: #16a34a; font-weight: 700; }
  .con { color: #dc2626; font-weight: 700; }
  .kv { display: flex; gap: 1rem; padding: 6px 0; border-bottom: 1px solid #f3f4f6; font-size: 14px; }
  .kv:last-child { border-bottom: none; }
  .kv-k { color: #6b7280; min-width: 150px; font-size: 13px; }
  .kv-v { color: #1a1a2e; flex: 1; }
  .cmd { display: inline-block; background: #1e2636; color: #56d364; font-family: 'SFMono-Regular', Consolas, monospace; font-size: 12px; padding: 4px 10px; border-radius: 6px; margin: 2px 0; }
  .svc-grid { display: grid; grid-template-columns: repeat(3, 1fr); gap: 0.75rem; }
  .svc-card { background: white; border: 1px solid #e5e7eb; border-radius: 10px; padding: 1rem; }
  .svc-name { font-size: 15px; font-weight: 700; margin-bottom: 2px; }
  .svc-use  { font-size: 12px; color: #6b7280; margin-bottom: 10px; }
  @media (max-width: 600px) {
    .svc-grid, .grid2 { grid-template-columns: 1fr; }
    .page { padding: 1.5rem 1rem 4rem; }
    .page-title { font-size: 1.4rem; }
  }
</style>
</head>
<body>
<div class="page">

  <div class="page-title">Kubernetes Networking</div>
  <div class="page-sub">Interview revision notes · Concepts → Service types → Ports → When to use</div>

  <!-- 1 -->
  <div class="section">
    <h2><span class="num">1</span> Container &amp; Pod</h2>
    <div class="grid2">
      <div class="card">
        <div class="card-label">Container</div>
        <p>Runs the application. The app listens on a specific port called the <strong>container port</strong> or <strong>target port</strong>.</p>
        <div class="kv" style="margin-top:8px;"><div class="kv-k">Java app</div><div class="kv-v"><code>8080</code></div></div>
        <div class="kv"><div class="kv-k">Nginx</div><div class="kv-v"><code>80</code></div></div>
      </div>
      <div class="card">
        <div class="card-label">Pod</div>
        <p>Smallest deployable unit. Can hold one or more containers. Each pod gets its own IP.</p>
        <div class="callout callout-warn" style="margin-top:8px;">
          <div class="callout-label">Pods are ephemeral</div>
          If a pod crashes, the new pod gets a new IP. <code>10.0.0.8</code> → <code>10.0.0.9</code>. Never talk to pod IPs directly — use a Service.
        </div>
      </div>
    </div>
  </div>

  <!-- 2 -->
  <div class="section">
    <h2><span class="num">2</span> Why Services Are Needed</h2>
    <div class="card">
      <p>Pods are ephemeral and their IPs change. A <strong>Service</strong> gives a stable front door.</p>
      <div style="display:grid; grid-template-columns:1fr 1fr; gap:4px; margin-top:8px;">
        <div class="pc"><span class="pro">✔</span> Stable IP address</div>
        <div class="pc"><span class="pro">✔</span> Stable DNS name</div>
        <div class="pc"><span class="pro">✔</span> Load balancing across pods</div>
        <div class="pc"><span class="pro">✔</span> Survives pod crashes &amp; restarts</div>
      </div>
    </div>
  </div>

  <!-- 3 -->
  <div class="section">
    <h2><span class="num">3</span> Labels &amp; Selectors</h2>
    <p style="margin-bottom:0.75rem;">This is how a Service knows which pods to send traffic to — even after a crash and restart.</p>
    <div class="grid2">
      <div class="card">
        <div class="card-label">Pod has a label</div>
        <div class="code-block">metadata:
  labels:
    <span class="hl-green">app: backend</span></div>
        <p style="font-size:13px; color:#6b7280;">Labels are key-value pairs on pods, like tags.</p>
      </div>
      <div class="card">
        <div class="card-label">Service has a selector</div>
        <div class="code-block">spec:
  selector:
    <span class="hl-blue">app: backend</span></div>
        <p style="font-size:13px; color:#6b7280;">Service only forwards to pods whose labels match.</p>
      </div>
    </div>
    <div class="callout callout-info">
      <div class="callout-label">How auto re-routing works</div>
      New pod starts → gets the same label → service selector matches → traffic automatically goes to the new pod. No manual update needed.
    </div>
  </div>

  <!-- 4 -->
  <div class="section">
    <h2><span class="num">4</span> Service Types</h2>
    <div class="svc-grid">
      <div class="svc-card" style="border-top:3px solid #3b82f6;">
        <div class="svc-name" style="color:#1d4ed8;">ClusterIP</div>
        <div class="svc-use">Internal only · Default type</div>
        <div class="flow"><div class="fn b">Frontend</div><div class="fa">→</div><div class="fn">Backend</div></div>
        <div class="flow"><div class="fn">Backend</div><div class="fa">→</div><div class="fn">Database</div></div>
        <p style="font-size:13px; color:#dc2626; margin-top:8px;">✗ External users cannot access</p>
      </div>
      <div class="svc-card" style="border-top:3px solid #f59e0b;">
        <div class="svc-name" style="color:#92400e;">NodePort</div>
        <div class="svc-use">External access · Opens port on every node</div>
        <div class="flow" style="flex-direction:column; align-items:flex-start;">
          <div style="display:flex; gap:5px; align-items:center;"><div class="fn a">User</div><div class="fa">→</div><div class="fn">NodePort</div></div>
          <div style="display:flex; gap:5px; align-items:center; margin-top:4px;"><div class="fn">Service</div><div class="fa">→</div><div class="fn">Pod</div><div class="fa">→</div><div class="fn">Container</div></div>
        </div>
        <p style="font-size:13px; color:#6b7280; margin-top:8px;">Port range: <code>30000–32767</code></p>
      </div>
      <div class="svc-card" style="border-top:3px solid #14b8a6;">
        <div class="svc-name" style="color:#0f766e;">LoadBalancer</div>
        <div class="svc-use">Cloud production · Public IP/DNS</div>
        <div class="flow" style="flex-direction:column; align-items:flex-start;">
          <div style="display:flex; gap:5px; align-items:center;"><div class="fn t">Internet</div><div class="fa">→</div><div class="fn">Cloud LB</div></div>
          <div style="display:flex; gap:5px; align-items:center; margin-top:4px;"><div class="fn">Service</div><div class="fa">→</div><div class="fn g">Pod</div></div>
        </div>
        <p style="font-size:13px; color:#dc2626; margin-top:8px;">✗ Not available in Kind (local)</p>
      </div>
    </div>
    <div class="card" style="margin-top:0.75rem; border-left:3px solid #8b5cf6; border-radius:0 10px 10px 0;">
      <div class="card-label">Ingress (advanced)</div>
      <p>HTTP/HTTPS routing layer in front of multiple services. Routes by domain or URL path. Needs an Ingress Controller (e.g. NGINX Ingress Controller).</p>
      <div class="flow" style="margin-top:8px;">
        <div class="fn" style="background:#faf5ff; border-color:#c4b5fd; color:#6d28d9;">Internet</div>
        <div class="fa">→</div><div class="fn">Ingress Controller</div>
        <div class="fa">→</div><div class="fn">/app1 → Svc A</div>
        <div class="fa">&amp;</div><div class="fn">/app2 → Svc B</div>
      </div>
    </div>
  </div>

  <!-- 5 -->
  <div class="section">
    <h2><span class="num">5</span> Port Reference</h2>
    <div class="card" style="padding:0; overflow:hidden;">
      <table>
        <thead>
          <tr><th>Port Name</th><th>Where it lives</th><th>What it does</th><th>Example</th></tr>
        </thead>
        <tbody>
          <tr>
            <td class="mono">containerPort</td>
            <td>Inside the Pod</td>
            <td>Where the app actually listens</td>
            <td><code>80</code>, <code>8080</code></td>
          </tr>
          <tr>
            <td class="mono">targetPort</td>
            <td>Pod (referenced by Service)</td>
            <td>Service forwards traffic here — usually same as containerPort</td>
            <td><code>8080</code></td>
          </tr>
          <tr>
            <td class="mono">port</td>
            <td>Service (inside cluster)</td>
            <td>The Service's "door" — other pods use this to talk to the service</td>
            <td><code>80</code></td>
          </tr>
          <tr>
            <td class="mono">nodePort</td>
            <td>Every worker node</td>
            <td>External port opened on each node for outside access</td>
            <td><code>30007</code></td>
          </tr>
        </tbody>
      </table>
    </div>
    <div class="callout callout-green" style="margin-top:0.75rem;">
      <div class="callout-label">Interview answer — ports</div>
      <strong>targetPort</strong> is where the app runs inside the container. The <strong>service port</strong> is used internally in the cluster — it forwards traffic to targetPort. Since pods are ephemeral, the service uses <strong>labels and selectors</strong> to route traffic. <strong>NodePort</strong> exposes the service externally on every worker node.
    </div>
  </div>

  <!-- 6 -->
  <div class="section">
    <h2><span class="num">6</span> Kind &amp; Extra Port Mappings</h2>
    <div class="card">
      <p>In Kind, Kubernetes runs <em>inside Docker containers</em>. NodePort only exposes within Docker's internal network — not on your actual machine. <code>extraPortMappings</code> bridges that gap.</p>
    </div>
    <div class="code-block"><span class="hl-muted"># kind-config.yaml</span>
extraPortMappings:
  - containerPort: <span class="hl-amber">30012</span>   <span class="hl-muted"># NodePort inside cluster</span>
    hostPort: <span class="hl-green">8080</span>       <span class="hl-muted"># port on your local machine</span></div>
    <div class="card">
      <div class="card-label">Full traffic flow — Kind + NodePort</div>
      <div class="flow" style="flex-direction:column; align-items:flex-start; gap:4px;">
        <div style="display:flex; align-items:center; gap:6px;">
          <div class="fn g">localhost:8080</div><div class="fa">→</div>
          <span style="font-size:12px; color:#6b7280;">your machine (hostPort)</span>
        </div>
        <div style="display:flex; align-items:center; gap:6px;">
          <div class="fn a">Kind node</div><div class="fa">→</div>
          <span style="font-size:12px; color:#6b7280;">extraPortMappings: hostPort 8080 → containerPort 30012</span>
        </div>
        <div style="display:flex; align-items:center; gap:6px;">
          <div class="fn b">NodePort Service</div><div class="fa">→</div>
          <span style="font-size:12px; color:#6b7280;">30012 → service port 80</span>
        </div>
        <div style="display:flex; align-items:center; gap:6px;">
          <div class="fn g">Pod (Nginx :80)</div><div class="fa">→</div>
          <span style="font-size:12px; color:#6b7280;">serves the page ✓</span>
        </div>
      </div>
    </div>
  </div>

  <!-- 7 -->
  <div class="section">
    <h2><span class="num">7</span> Access Methods</h2>
    <div class="card" style="margin-bottom:0.75rem;">
      <div style="display:flex; align-items:center; gap:8px; margin-bottom:8px;"><span class="tag tag-amber">NodePort</span><strong>Persistent access through the node</strong></div>
      <div class="flow" style="margin-bottom:8px;">
        <div class="fn g">localhost:8080</div><div class="fa">→</div>
        <div class="fn a">NodePort :30012</div><div class="fa">→</div>
        <div class="fn">Service :80</div><div class="fa">→</div>
        <div class="fn g">Pod :80</div>
      </div>
      <div class="pc"><span class="pro">✔</span> Persistent — stays up even after terminal closes</div>
      <div class="pc"><span class="con">✗</span> Requires cluster config changes (extraPortMappings in Kind)</div>
    </div>
    <div class="card" style="margin-bottom:0.75rem;">
      <div style="display:flex; align-items:center; gap:8px; margin-bottom:8px;"><span class="tag tag-blue">Port Forward</span><strong>Quick temporary tunnel — dev &amp; debugging</strong></div>
      <div class="cmd">kubectl port-forward svc/myappservice 8080:80</div>
      <div class="flow" style="margin:8px 0;">
        <div class="fn b">localhost:8080</div><div class="fa">→</div>
        <div class="fn">Service :80</div><div class="fa">→</div>
        <div class="fn g">Pod :80</div>
      </div>
      <div class="pc"><span class="pro">✔</span> No cluster config needed — great for debugging</div>
      <div class="pc"><span class="con">✗</span> Temporary — tunnel dies when you stop the command</div>
      <div class="pc"><span class="con">✗</span> Only accessible from your local machine</div>
    </div>
    <div class="card">
      <div style="display:flex; align-items:center; gap:8px; margin-bottom:8px;"><span class="tag tag-teal">LoadBalancer</span><strong>Cloud production — public IP or DNS</strong></div>
      <div class="flow" style="margin-bottom:8px;">
        <div class="fn t">Internet</div><div class="fa">→</div>
        <div class="fn">Cloud LB</div><div class="fa">→</div>
        <div class="fn">Service</div><div class="fa">→</div>
        <div class="fn g">Pod</div>
      </div>
      <div class="pc"><span class="pro">✔</span> Best for exposing apps to the internet in cloud clusters</div>
      <div class="pc"><span class="con">✗</span> Not available in Kind / local Docker</div>
    </div>
  </div>

  <!-- 8 -->
  <div class="section">
    <h2><span class="num">8</span> When to Use What</h2>
    <div class="card" style="padding:0; overflow:hidden;">
      <table>
        <thead><tr><th>Situation</th><th>Use</th><th>Reason</th></tr></thead>
        <tbody>
          <tr>
            <td>Dev / debugging</td>
            <td><span class="tag tag-blue">Port Forward</span></td>
            <td>Fast, zero config, no cluster changes</td>
          </tr>
          <tr>
            <td>Local persistent access (Kind)</td>
            <td><span class="tag tag-amber">NodePort</span></td>
            <td>Add extraPortMappings in Kind config</td>
          </tr>
          <tr>
            <td>Cloud production (single app)</td>
            <td><span class="tag tag-teal">LoadBalancer</span></td>
            <td>Cloud-managed public IP / DNS</td>
          </tr>
          <tr>
            <td>Cloud production (multiple apps)</td>
            <td><span class="tag tag-purple">Ingress</span></td>
            <td>TLS, host/path routing, one entry point</td>
          </tr>
          <tr>
            <td>Internal service-to-service</td>
            <td><span class="tag tag-blue">ClusterIP</span></td>
            <td>Default — no external exposure needed</td>
          </tr>
        </tbody>
      </table>
    </div>
  </div>

  <!-- 9 -->
  <div class="section">
    <h2><span class="num">9</span> Quick kubectl Commands</h2>
    <div class="card">
      <div class="kv"><div class="kv-k">List pods by label</div><div class="kv-v"><span class="cmd">kubectl get pods -l app=myapp</span></div></div>
      <div class="kv"><div class="kv-k">Check service</div><div class="kv-v"><span class="cmd">kubectl get svc myappservice</span></div></div>
      <div class="kv"><div class="kv-k">Port forward</div><div class="kv-v"><span class="cmd">kubectl port-forward svc/myappservice 8080:80</span></div></div>
      <div class="kv"><div class="kv-k">Test NodePort</div><div class="kv-v"><span class="cmd">curl http://localhost:8080</span></div></div>
      <div class="kv"><div class="kv-k">Test LoadBalancer</div><div class="kv-v"><span class="cmd">curl http://&lt;EXTERNAL-IP&gt;</span></div></div>
    </div>
  </div>

  <!-- Memory shortcut -->
  <div class="callout callout-purple">
    <div class="callout-label">Quick memory — say this before the interview</div>
    <div style="display:flex; flex-direction:column; gap:5px; font-size:14px;">
      <div><strong>ClusterIP</strong> — internal only, default, service-to-service communication</div>
      <div><strong>NodePort</strong> — permanent door on the node (needs extraPortMappings in Kind)</div>
      <div><strong>Port Forward</strong> — temporary tunnel to a Service or Pod, great for debugging</div>
      <div><strong>LoadBalancer</strong> — cloud-provided public IP or DNS, production use</div>
      <div><strong>Ingress</strong> — smart HTTP router, multiple apps under one entry point</div>
    </div>
  </div>

  <div style="margin-top:2rem; font-size:12px; color:#9ca3af; text-align:center; padding-top:1rem; border-top:1px solid #e5e7eb;">
    Kubernetes Networking · Interview Revision Notes
  </div>

</div>
</body>
</html>
