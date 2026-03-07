---
# the default layout is 'page'
title: Idea Map
icon: fas fa-diagram-project
order: 3
---

<div class="idea-map-app">
  <section class="idea-map-sidebar">
    <h2>Projects</h2>
    <form id="project-form" class="idea-map-form">
      <label for="project-name">New project</label>
      <div class="idea-map-row">
        <input id="project-name" type="text" maxlength="80" placeholder="Ex: Portfolio redesign" required />
        <button type="submit">Add</button>
      </div>
    </form>

    <ul id="project-list" class="project-list" aria-live="polite"></ul>
  </section>

  <section class="idea-map-main">
    <div id="empty-state" class="empty-state">
      <h2>Your idea map starts here</h2>
      <p>Create a project from the left to start mapping ideas, notes, and screenshots.</p>
    </div>

    <article id="project-view" class="project-view" hidden>
      <header class="project-header">
        <div>
          <p class="project-tag">Active project</p>
          <h2 id="project-title"></h2>
          <p id="project-created" class="meta"></p>
        </div>
        <button id="delete-project" class="danger">Delete project</button>
      </header>

      <section class="panel">
        <h3>Add note</h3>
        <form id="note-form" class="idea-map-form">
          <textarea id="note-text" rows="4" maxlength="500" placeholder="Capture what this idea needs next..." required></textarea>
          <button type="submit">Save note</button>
        </form>
      </section>

      <section class="panel">
        <h3>Add screenshot</h3>
        <form id="screenshot-form" class="idea-map-form">
          <input id="screenshot-input" type="file" accept="image/*" required />
          <button type="submit">Attach screenshot</button>
        </form>
      </section>

      <section class="panel">
        <h3>Notes</h3>
        <ul id="notes-list" class="content-list"></ul>
      </section>

      <section class="panel">
        <h3>Screenshots</h3>
        <div id="images-grid" class="images-grid"></div>
      </section>
    </article>
  </section>
</div>

<style>
.idea-map-app {
  display: grid;
  grid-template-columns: minmax(240px, 320px) 1fr;
  gap: 1.25rem;
  align-items: start;
}

.idea-map-sidebar,
.panel,
.project-view,
.empty-state {
  border: 1px solid var(--card-border-color, rgba(128, 128, 128, 0.25));
  border-radius: 12px;
  background: var(--card-bg, rgba(127, 127, 127, 0.06));
}

.idea-map-sidebar {
  padding: 1rem;
  position: sticky;
  top: 1rem;
}

.idea-map-main {
  min-width: 0;
}

.empty-state {
  padding: 2rem;
}

.project-view {
  padding: 1rem;
  display: grid;
  gap: 1rem;
}

.project-header {
  display: flex;
  align-items: start;
  justify-content: space-between;
  gap: 1rem;
}

.project-tag {
  font-size: 0.8rem;
  text-transform: uppercase;
  letter-spacing: 0.08em;
  opacity: 0.75;
  margin-bottom: 0.25rem;
}

.meta {
  opacity: 0.8;
  margin: 0;
}

.idea-map-form {
  display: grid;
  gap: 0.5rem;
}

.idea-map-row {
  display: flex;
  gap: 0.5rem;
}

.idea-map-row input {
  flex: 1;
}

button,
input,
textarea {
  font: inherit;
}

button {
  border: 1px solid transparent;
  border-radius: 8px;
  padding: 0.5rem 0.75rem;
  cursor: pointer;
  background: var(--btn-bg, #2d68ff);
  color: #fff;
}

button:hover {
  opacity: 0.9;
}

button.danger {
  background: #b42318;
}

input[type="text"],
textarea,
input[type="file"] {
  border: 1px solid var(--card-border-color, rgba(128, 128, 128, 0.3));
  border-radius: 8px;
  padding: 0.5rem 0.65rem;
  background: var(--card-bg, rgba(127, 127, 127, 0.08));
  color: inherit;
}

.project-list,
.content-list {
  list-style: none;
  margin: 1rem 0 0;
  padding: 0;
  display: grid;
  gap: 0.5rem;
}

.project-list button {
  width: 100%;
  text-align: left;
  background: transparent;
  border-color: var(--card-border-color, rgba(128, 128, 128, 0.3));
  color: inherit;
}

.project-list button.active {
  border-color: #2d68ff;
  box-shadow: inset 0 0 0 1px #2d68ff;
}

.panel {
  padding: 1rem;
}

.content-item {
  border: 1px solid var(--card-border-color, rgba(128, 128, 128, 0.25));
  border-radius: 8px;
  padding: 0.75rem;
  display: grid;
  gap: 0.5rem;
}

.content-item-header {
  display: flex;
  justify-content: space-between;
  align-items: center;
  gap: 0.5rem;
}

.content-item-header button {
  background: transparent;
  color: inherit;
  border-color: var(--card-border-color, rgba(128, 128, 128, 0.3));
  padding: 0.2rem 0.5rem;
}

.images-grid {
  display: grid;
  gap: 0.75rem;
  grid-template-columns: repeat(auto-fit, minmax(150px, 1fr));
}

.images-grid figure {
  margin: 0;
  border: 1px solid var(--card-border-color, rgba(128, 128, 128, 0.25));
  border-radius: 8px;
  overflow: hidden;
  background: rgba(127, 127, 127, 0.08);
}

.images-grid img {
  width: 100%;
  height: 140px;
  object-fit: cover;
  display: block;
}

.images-grid figcaption {
  padding: 0.45rem 0.55rem;
  font-size: 0.85rem;
}

@media (max-width: 900px) {
  .idea-map-app {
    grid-template-columns: 1fr;
  }

  .idea-map-sidebar {
    position: static;
  }
}
</style>

<script>
(() => {
  const STORAGE_KEY = 'idea-map-projects-v1';
  const state = {
    projects: [],
    activeProjectId: null
  };

  const projectForm = document.getElementById('project-form');
  const projectNameInput = document.getElementById('project-name');
  const projectList = document.getElementById('project-list');
  const emptyState = document.getElementById('empty-state');
  const projectView = document.getElementById('project-view');
  const projectTitle = document.getElementById('project-title');
  const projectCreated = document.getElementById('project-created');
  const deleteProjectBtn = document.getElementById('delete-project');
  const noteForm = document.getElementById('note-form');
  const noteInput = document.getElementById('note-text');
  const notesList = document.getElementById('notes-list');
  const screenshotForm = document.getElementById('screenshot-form');
  const screenshotInput = document.getElementById('screenshot-input');
  const imagesGrid = document.getElementById('images-grid');

  function saveState() {
    localStorage.setItem(STORAGE_KEY, JSON.stringify(state.projects));
  }

  function loadState() {
    const raw = localStorage.getItem(STORAGE_KEY);
    if (!raw) return;

    try {
      const projects = JSON.parse(raw);
      if (Array.isArray(projects)) {
        state.projects = projects;
        state.activeProjectId = projects[0]?.id ?? null;
      }
    } catch (error) {
      console.warn('Failed to parse idea map data', error);
    }
  }

  function formatDate(timestamp) {
    return new Date(timestamp).toLocaleString();
  }

  function getActiveProject() {
    return state.projects.find((project) => project.id === state.activeProjectId) ?? null;
  }

  function removeById(list, id) {
    return list.filter((item) => item.id !== id);
  }

  function renderProjectList() {
    projectList.innerHTML = '';

    if (state.projects.length === 0) {
      const li = document.createElement('li');
      li.textContent = 'No projects yet.';
      projectList.append(li);
      return;
    }

    state.projects.forEach((project) => {
      const li = document.createElement('li');
      const button = document.createElement('button');
      button.type = 'button';
      button.textContent = project.name;
      button.className = project.id === state.activeProjectId ? 'active' : '';
      button.addEventListener('click', () => {
        state.activeProjectId = project.id;
        render();
      });
      li.append(button);
      projectList.append(li);
    });
  }

  function renderProject() {
    const project = getActiveProject();

    if (!project) {
      emptyState.hidden = false;
      projectView.hidden = true;
      return;
    }

    emptyState.hidden = true;
    projectView.hidden = false;
    projectTitle.textContent = project.name;
    projectCreated.textContent = `Created ${formatDate(project.createdAt)}`;

    notesList.innerHTML = '';
    if (project.notes.length === 0) {
      const li = document.createElement('li');
      li.textContent = 'No notes yet.';
      notesList.append(li);
    } else {
      project.notes.forEach((note) => {
        const li = document.createElement('li');
        li.className = 'content-item';

        const header = document.createElement('div');
        header.className = 'content-item-header';
        header.innerHTML = `<small>${formatDate(note.createdAt)}</small>`;

        const removeBtn = document.createElement('button');
        removeBtn.type = 'button';
        removeBtn.textContent = 'Remove';
        removeBtn.addEventListener('click', () => {
          project.notes = removeById(project.notes, note.id);
          saveState();
          render();
        });

        header.append(removeBtn);

        const body = document.createElement('p');
        body.textContent = note.text;

        li.append(header, body);
        notesList.append(li);
      });
    }

    imagesGrid.innerHTML = '';
    if (project.images.length === 0) {
      imagesGrid.textContent = 'No screenshots yet.';
    } else {
      project.images.forEach((image) => {
        const figure = document.createElement('figure');
        const img = document.createElement('img');
        img.src = image.dataUrl;
        img.alt = image.name;

        const caption = document.createElement('figcaption');
        caption.textContent = `${image.name} • ${formatDate(image.createdAt)}`;

        const removeBtn = document.createElement('button');
        removeBtn.type = 'button';
        removeBtn.className = 'danger';
        removeBtn.textContent = 'Remove';
        removeBtn.addEventListener('click', () => {
          project.images = removeById(project.images, image.id);
          saveState();
          render();
        });

        caption.append(document.createElement('br'), removeBtn);
        figure.append(img, caption);
        imagesGrid.append(figure);
      });
    }
  }

  function render() {
    renderProjectList();
    renderProject();
  }

  projectForm.addEventListener('submit', (event) => {
    event.preventDefault();
    const name = projectNameInput.value.trim();

    if (!name) return;

    const project = {
      id: crypto.randomUUID(),
      name,
      createdAt: Date.now(),
      notes: [],
      images: []
    };

    state.projects.unshift(project);
    state.activeProjectId = project.id;
    projectForm.reset();
    saveState();
    render();
  });

  deleteProjectBtn.addEventListener('click', () => {
    const project = getActiveProject();
    if (!project) return;

    state.projects = removeById(state.projects, project.id);
    state.activeProjectId = state.projects[0]?.id ?? null;
    saveState();
    render();
  });

  noteForm.addEventListener('submit', (event) => {
    event.preventDefault();
    const project = getActiveProject();
    const text = noteInput.value.trim();

    if (!project || !text) return;

    project.notes.unshift({
      id: crypto.randomUUID(),
      text,
      createdAt: Date.now()
    });

    noteForm.reset();
    saveState();
    render();
  });

  screenshotForm.addEventListener('submit', (event) => {
    event.preventDefault();
    const project = getActiveProject();
    const file = screenshotInput.files?.[0];

    if (!project || !file) return;

    const reader = new FileReader();
    reader.onload = () => {
      project.images.unshift({
        id: crypto.randomUUID(),
        name: file.name,
        createdAt: Date.now(),
        dataUrl: String(reader.result)
      });

      screenshotForm.reset();
      saveState();
      render();
    };

    reader.readAsDataURL(file);
  });

  loadState();
  render();
})();
</script>
