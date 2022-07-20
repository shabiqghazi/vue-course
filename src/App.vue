<template>
  <div class="container mb-5">
    <p v-html="content"></p>
    <p v-text="text" :id="textId"></p>
    <p
      :class="{
        done: isDone,
        left: !isLeft,
        urgent: !isUrgent,
      }"
    >
      Tugas 1 (selesai)
    </p>
    <p
      :class="{
        done: !isDone,
        left: !isLeft,
        urgent: isUrgent,
      }"
    >
      Tugas 2 (belum selesai)
    </p>
    <p
      :class="{
        done: !isDone,
        left: isLeft,
        urgent: !isUrgent,
      }"
    >
      Tugas 3 (terlewat)
    </p>
    <p :class="[isDone && 'done', isUrgent && 'urgent']">Tugas 4 (selesai)</p>
    <div :style="[baseBox]" v-if="ph === 7">Light Box</div>
    <div :style="[baseBox, successBox]" v-else-if="ph < 7">Success box</div>
    <div :style="[baseBox, dangerBox]" v-else>Danger box</div>

    <div :style="[baseBox, dangerBox]" v-show="true">Don't click</div>

    <template v-if="showAll">
      <div :style="[baseBox, successBox]">Success</div>
      <div :style="[baseBox, dangerBox]">Danger</div>
    </template>
    <hr />
    <h2 v-for="(name, index) in names" :key="index">
      {{ index + 1 }}. {{ name }}
    </h2>

    <table
      border="1"
      cellspacing="0"
      cellpadding="5"
      :style="{ display: 'inline-block' }"
    >
      <tr>
        <th>#</th>
        <th>Name</th>
        <th>NIM</th>
        <th>GPA</th>
        <th>Title</th>
      </tr>
      <template v-for="(student, index) in students" :key="index">
        <tr v-if="student.gpa >= 3.5">
          <td>{{ index + 1 }}</td>
          <td>{{ student.name }}</td>
          <td>{{ student.nim }}</td>
          <td>{{ student.gpa }}</td>
          <td>
            <template v-for="title in student.titles">{{ title }}, </template>
          </td>
        </tr>
      </template>
    </table>

    <div v-for="(value, key, index) in team" :key="index">
      <h3>{{ key }} : {{ value }}</h3>
    </div>
    <hr />
    <h3>4 + 3 = {{ sum(4, 3) }}</h3>
    <h4>3 * 3 = {{ pow(3) }}</h4>
    <h3>{{ sayHello() }}</h3>

    <hr />
    <h1>Event Handling</h1>
    <h1>
      Count : {{ count }} <span>{{ badge }}</span>
    </h1>
    <button @click="changeCount($event), changeBadge('Changed Up!')" num="1">
      Increment 1
    </button>
    <button @click="changeCount($event), changeBadge('Changed Up!')" num="5">
      Increment 5
    </button>
    <button @click="changeCount($event), changeBadge('Changed Down!')" num="-1">
      Decrement 1
    </button>
    <button @click="changeCount($event), changeBadge('Changed Down!')" num="-5">
      Decrement 5
    </button>

    <hr />
    <div class="container col-4">
      <h1>Form Handling</h1>
      <form class="mt-5" @submit="handleSubmit">
        <div class="mb-3">
          <label for="nama" class="form-label">Nama</label>
          <input
            type="text"
            class="form-control"
            id="nama"
            v-model.trim="formValues.nama"
          />
        </div>
        <div class="mb-3">
          <label for="deskripsi" class="form-label">Deskripsi</label>
          <textarea
            class="form-control"
            id="deskripsi"
            rows="3"
            v-model.lazy="formValues.deskripsi"
          />
        </div>
        <div class="mb-3">
          <label for="posisi" class="form-label">Posisi</label>
          <select class="form-select" v-model="formValues.posisi">
            <option value="">Open this select menu</option>
            <option value="frontend">Front-end Developer</option>
            <option value="backend">Back-end Developer</option>
            <option value="mobile">Mobile Developer</option>
          </select>
        </div>
        <div class="mb-3">
          <label for="skills" class="form-label">Keahlian</label>
          <select class="form-select" multiple v-model="formValues.skills">
            <option value="">Open this select menu</option>
            <option value="slicing">Slicing</option>
            <option value="state-management">State Management</option>
            <option value="rest-api">Rest API</option>
          </select>
        </div>
        <div class="form-check mb-3">
          <input
            class="form-check-input"
            type="checkbox"
            v-model="formValues.isFreshGraduate"
            id="fresh-graduate"
            true-value="yes"
            false-value="no"
          />
          <label class="form-check-label" for="fresh-graduate">
            Fresh Graduate
          </label>
        </div>
        <div class="form-check">
          <input
            class="form-check-input"
            type="checkbox"
            id="public-speaking"
            value="public-speaking"
            v-model="formValues.specialSkills"
          />
          <label class="form-check-label" for="public-speaking">
            Public Speaking
          </label>
        </div>
        <div class="form-check">
          <input
            class="form-check-input"
            type="checkbox"
            id="time-management"
            value="time-management"
            v-model="formValues.specialSkills"
          />
          <label class="form-check-label" for="time-management">
            Time Management
          </label>
        </div>
        <div class="form-check">
          <input
            class="form-check-input"
            type="checkbox"
            id="leadership"
            value="leadership"
            v-model="formValues.specialSkills"
          />
          <label class="form-check-label" for="leadership"> Leadership </label>
        </div>
        <div class="form-check form-check-inline">
          <input
            class="form-check-input"
            type="radio"
            id="0-2"
            value="0-2"
            v-model="formValues.experience"
          />
          <label class="form-check-label" for="0-2">0-2</label>
        </div>
        <div class="form-check form-check-inline">
          <input
            class="form-check-input"
            type="radio"
            id="3-4"
            value="3-4"
            v-model="formValues.experience"
          />
          <label class="form-check-label" for="3-4">3-4</label>
        </div>
        <div class="form-check form-check-inline">
          <input
            class="form-check-input"
            type="radio"
            id="4+"
            value="4+"
            v-model="formValues.experience"
          />
          <label class="form-check-label" for="4+">4+</label>
        </div>
        <div class="mb-3">
          <label for="age" class="form-label">Age</label>
          <input
            type="number"
            class="form-control"
            id="age"
            v-model.number="formValues.age"
          />
        </div>
        <div class="mb-3">
          <button type="submit" class="btn btn-primary">Submit</button>
        </div>
      </form>
      <div>
        <pre>
      {{ JSON.stringify(formValues, null, 2) }}
    </pre
        >
      </div>
    </div>
    <hr />
    <div class="container col-4" v-once>
      <h1>Bonus Directives</h1>
      Jumlah : {{ count }}
      <button class="btn btn-primary" @click="changeCount" num="1">
        Tambah 1
      </button>
      <br />
      <p v-pre>
        {{ content }}
      </p>
    </div>
    <hr />
    <h1>Computed Properties</h1>
    <h3>Hi, {{ firstName }} {{ lastName }}</h3>
    <h4>{{ fullName }}</h4>
    <button @click="changeName">Change Name</button>
    <div class="col-6">
      <table class="table">
        <thead>
          <tr>
            <th scope="col">#</th>
            <th scope="col">Nama</th>
            <th scope="col">NIM</th>
            <th scope="col">IPK</th>
          </tr>
        </thead>
        <tbody>
          <tr v-for="(student, index) in cumlaudeStudents" :key="student.nim">
            <td scope="row">{{ index + 1 }}</td>
            <td>{{ student.name }}</td>
            <td>{{ student.nim }}</td>
            <td>{{ student.gpa }}</td>
          </tr>
        </tbody>
      </table>
    </div>
    <hr />
    <h1>Watchers</h1>
    <div class="col-4">
      <label for="volume" class="form-label">Volume : {{ volume }} </label>
      <input
        type="range"
        class="form-range"
        min="0"
        max="20"
        step="2"
        v-model.number="volume"
        id="volume"
      />
      <div class="mb-3">
        <label for="movie" class="form-label">Movie Name</label>
        <input
          type="text"
          class="form-control"
          id="movie"
          v-model.trim="movie"
        />
      </div>
      <div class="mb-3">
        <label for="movie-title" class="form-label">Movie Title</label>
        <input
          type="text"
          class="form-control"
          id="movie-title"
          v-model.trim="movieInfo.title"
        />
      </div>
      <div class="mb-3">
        <label for="movie-actor" class="form-label">Movie Actor</label>
        <input
          type="text"
          class="form-control"
          id="movie-actor"
          v-model.trim="movieInfo.actor"
        />
      </div>
      <div class="mb-3">
        <label for="movie-actor" class="form-label">Movie List</label>
        <p v-for="(movie, index) in movieList" :key="index">
          {{ index+1 }}. {{ movie }}
        </p>
        <button class="btn btn-primary" @click="movieList.push('KKN di Desa Penari')">Add Film</button>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "App",
  data() {
    return {
      pow: (num) => {
        return num * num;
      },
      badge: "",
      count: 0,
      content: "<span>Shabiq Ghazi Arkaan</span>",
      text: "Front-end web developer",
      textId: "text",
      buttonDisabled: true,
      isDone: true,
      isLeft: true,
      isUrgent: true,
      ph: 7,
      showAll: true,

      names: ["Shabiq", "Ghazi", "Arkaan"],
      students: [
        {
          name: "Shabiq Ghazi Arkaan",
          nim: 1207050118,
          gpa: 3.46,
          titles: ["Kosma", "Best Kosma", "Mahasiswa Inspiratif"],
        },
        {
          name: "Mohammad Ahsan",
          nim: 1207050134,
          gpa: 4.0,
          titles: ["BWC Champions 2019"],
        },
        {
          name: "Hendra Setiawan",
          nim: 1207050135,
          gpa: 3.99,
          titles: ["Olympic 2008 Champions"],
        },
        {
          name: "Anthony Sinisuka Ginting",
          nim: 1207050136,
          gpa: 3.08,
          titles: ["Badminton Singapore Open 2022 Champions"],
        },
      ],
      team: {
        name: "Persib Bandung",
        coach: "Robert Rene Alberts",
        stadium: "Si Jalak Harupat",
      },

      baseBox: {
        display: "inline-block",
        padding: "10px",
        maxWidth: "300px",
        borderRadius: "5px",
        margin: "0 5px",
        boxShadow: "0 5px 10px 2px rgba(0,0,0,0.2)",
        border: "1px solid grey",
        backgroundColor: "#eee",
      },
      successBox: {
        color: "green",
        border: "1px solid green",
        backgroundColor: "lightgreen",
      },
      dangerBox: {
        color: "brown",
        border: "1px solid brown",
        backgroundColor: "lightcoral",
      },

      formValues: {
        nama: "",
        deskripsi: "",
        posisi: "",
        skills: [],
        isFreshGraduate: "no",
        specialSkills: [],
        experience: "",
        age: null,
      },
      firstName: "Shabiq",
      lastName: "Ghazi Arkaan",

      volume: 10,
      movie: '',
      movieInfo: {
        title : '',
        actor: '',
      },
      movieList: ['Laskar Pelangi', 'Dilan 1990', 'Ayat-ayat Cinta']
    };
  },
  methods: {
    sum(a, b) {
      return a + b;
    },
    sayHello() {
      return `Hello ${this.text}`;
    },
    changeCount(event) {
      this.count += parseInt(event.target.attributes.num.value);
    },
    changeBadge(str) {
      this.badge = str;
    },
    handleSubmit(event) {
      event.preventDefault();
      console.log(this.formValues);
    },
    changeName() {
      this.fullName = "Mohammad Ahsan";
    },
  },
  computed: {
    fullName: {
      get() {
        return `${this.firstName} ${this.lastName}`;
      },
      set(fullName) {
        const names = fullName.split(" ");
        this.firstName = names[0];
        this.lastName = names[1];
      },
    },
    cumlaudeStudents() {
      return this.students.filter((student) => student.gpa > 3.5);
    },
  },
  watch: {
    volume(newValue, oldValue) {
      newValue === 16 && oldValue < 16
        ? alert("Volume yang terlalu besar dapat mengganggu pendengaran")
        : "";
    },
    movie : {
      handler(newValue) {
        console.log("Getting data from API for " + newValue)
      },
      immediate : true
    },
    movieInfo : {
      handler(newValue) {
        console.log(`Getting data with title = ${newValue.title} and actor = ${newValue.actor}`);
      },
      deep: true
    },
    movieList: {
      handler(newValue){
        console.log(newValue)
      },
      deep:true
    }
  },
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  /* text-align: center; */
  color: #2c3e50;
  margin-top: 60px;
}

#text {
  text-decoration: underline;
}
.done {
  color: chartreuse;
}
.left {
  color: crimson;
}
.urgent {
  text-decoration: underline;
  font-style: italic;
}
</style>
