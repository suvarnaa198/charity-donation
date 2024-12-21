<template>
  <div>
  <div class="dashboard">
    <h1>User Dashboard</h1>

    <!-- Sidebar Menu -->
    <aside class="sidebar">
      <ul>
        <li @click="navigate('profile')">My Profile</li>
        <li @click="navigate('fundraisers')">My Fundraisers</li>
        <li @click="navigate('donations')">My Donations</li>
        <li @click="navigate('create')">Create Fundraiser</li>
        <li @click="logout">Logout</li>
      </ul>
    </aside>

    <!-- Main Content -->
    <main>
      <section v-if="currentView === 'profile'">
        <h2>Dashboard Summary</h2>
        <p>Funds Raised: {{ summary.fundsRaised }}</p>
        <p>Campaigns Supported: {{ summary.campaignsSupported }}</p>
        <h3>Recent Activity</h3>
        <ul>
          <li v-for="activity in recentActivities" :key="activity.id">{{ activity.details }}</li>
        </ul>
      </section>

      <section v-if="currentView === 'create'">
        <h2>Create Fundraiser</h2>
        <form v-if="createStep === 1" @submit.prevent="nextStep">
          <label>Fundraiser Title</label>
          <input type="text" v-model="newFundraiser.title" required />

          <label>Description</label>
          <textarea v-model="newFundraiser.description" required></textarea>

          <label>Category</label>
          <select v-model="newFundraiser.category" required>
            <option v-for="category in categories" :key="category" :value="category">{{ category }}</option>
          </select>

          <button type="submit">Next</button>
          <button type="button" @click="cancelCreation">Cancel</button>
        </form>

        <form v-if="createStep === 2" @submit.prevent="submitFundraiser">
          <label>Target Amount</label>
          <input type="number" v-model="newFundraiser.target" required />

          <label>Minimum Donation</label>
          <input type="number" v-model="newFundraiser.minDonation" required />

          <label>End Date</label>
          <input type="date" v-model="newFundraiser.endDate" required />

          <label>Media Upload</label>
          <input type="file" multiple @change="uploadMedia" />

          <button type="submit">Submit</button>
          <button type="button" @click="previousStep">Back</button>
        </form>
      </section>

      <section v-if="currentView === 'campaign'">
        <h2>{{ campaignDetails.title }} ({{ campaignDetails.category }})</h2>
        <p>Time Remaining: {{ campaignDetails.timeLeft }}</p>
        <p>{{ campaignDetails.description }}</p>

        <progress :value="campaignDetails.progress" max="100"></progress>

        <div class="donation-box">
          <label>Donation Amount</label>
          <input type="number" v-model="donationAmount" required />
          <button @click="donate">Donate Now</button>
        </div>

        <h3>Media Gallery</h3>
        <div class="media-carousel">
          <img v-for="media in campaignDetails.media" :src="media" :key="media" alt="Campaign Media" />
        </div>

        <h3>Recent Donors</h3>
        <ul>
          <li v-for="donor in campaignDetails.donors" :key="donor.name">
            {{ donor.name }} donated {{ donor.amount }} at {{ donor.time }}
          </li>
        </ul>

        <h3>Share This Campaign</h3>
        <div class="social-links">
        </div>
      </section>
    </main>
  </div>
  </div>
</template>

<script>
export default {
  name: 'UserComponent',
  data() {
    return {
      currentView: 'profile',
      createStep: 1,
      summary: { fundsRaised: 5000, campaignsSupported: 10 },
      recentActivities: [{ id: 1, details: 'Donated to School Project' }],
      categories: ['Health', 'Education', 'Environment'],
      newFundraiser: {
        title: '',
        description: '',
        category: '',
        target: 0,
        minDonation: 0,
        endDate: '',
        media: []
      },
      campaignDetails: {
        title: 'Save the Rainforest',
        category: 'Environment',
        description: 'Help protect the rainforest.',
        progress: 75,
        timeLeft: '5 Days',
        media: ['image1.jpg', 'image2.jpg'],
        donors: [
          { name: 'John Doe', amount: 100, time: '2 hours ago' }
        ]
      },
      donationAmount: 0,
      socialLinks: [
        { platform: 'Facebook', url: '#' },
        { platform: 'Twitter', url: '#' }
      ]
    };
  },
  methods: {
    navigate(view) {
      this.currentView = view;
    },
    nextStep() {
      this.createStep = 2;
    },
    previousStep() {
      this.createStep = 1;
    },
    cancelCreation() {
      this.currentView = 'profile';
    },
    submitFundraiser() {
      alert('Fundraiser Created!');
    },
    donate() {
      alert(`Donated ${this.donationAmount}!`);
    },
    uploadMedia(event) {
      this.newFundraiser.media = Array.from(event.target.files);
    },
    logout() {
      alert('Logged out');
    }
  }

};
</script>
