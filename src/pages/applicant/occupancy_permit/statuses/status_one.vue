<template>
  <v-app class="page-wrapper">
    <v-navigation-drawer app permanent width="350">
      <div class="sidebar-content">
        <h2 class="guide-title">Quick Guide</h2>
        <p class="guide-subtitle">Follow these steps to complete your application</p>

        <div class="stepper-container mt-8">
          <div v-for="(step, index) in steps" :key="index" class="step-item">
            <div class="step-circle">{{ index + 1 }}</div>
            <div class="step-text">{{ step.text }}</div>
          </div>
        </div>

        <v-btn color="#2962FF" dark class="mt-8 download-btn">
          Download Complete Checklist
        </v-btn>

        <v-spacer></v-spacer>
        <v-btn text class="logout-btn mt-6">
          <v-icon left>mdi-logout</v-icon>
          Logout
        </v-btn>
      </div>
    </v-navigation-drawer>

    <v-main>
      <div class="main-content-wrapper">
        <div class="page-header">
          <v-icon class="me-3" color="#2962FF">mdi-office-building-outline</v-icon>
          <span class="page-title">Occupancy Permit Application</span>
          <v-spacer></v-spacer>
          <v-badge bordered color="red" content="1" offset-x="10" offset-y="10">
            <v-btn icon>
              <v-icon>mdi-bell-outline</v-icon>
            </v-btn>
          </v-badge>
          <div class="permit-info ms-4">
            <span class="permit-label">Building Permit Number</span>
            <span class="permit-id">BP-2025-0808-001</span>
          </div>
        </div>

        <div class="content-panel">
          <v-card class="application-info-card" outlined>
            <v-card-text class="d-flex align-center flex-wrap">
              <div class="info-left">
                <span class="info-title">Application {{ applicationInfo.id }}</span>
                <div class="info-details-grid">
                  <div>
                    <div class="detail-label">Submission Date</div>
                    <div class="detail-value">
                      {{ applicationInfo.submissionDate }}
                    </div>
                  </div>
                  <div>
                    <div class="detail-label">Application Type</div>
                    <div class="detail-value">
                      {{ applicationInfo.type }}
                    </div>
                  </div>
                  <div>
                    <div class="detail-label">Current Status</div>
                    <div class="detail-value">
                      {{ applicationInfo.status }}
                    </div>
                  </div>
                  <div>
                    <div class="detail-label">Last Updated</div>
                    <div class="detail-value">
                      {{ applicationInfo.lastUpdated }}
                    </div>
                  </div>
                </div>
              </div>
              <v-spacer></v-spacer>
              <span class="info-id-right">{{ applicationInfo.id }}</span>
            </v-card-text>
          </v-card>

          <div class="status-tracker-container mt-8">
            <h2 class="tracker-title">Application Status Tracker</h2>
            <div class="status-timeline-container">
              <div v-for="(item, index) in statusItems" :key="index" class="status-item">
                <div
                  class="status-icon-wrapper"
                  :class="item.status.toLowerCase().replace(' ', '-')"
                >
                  <v-icon :color="item.color">{{ item.icon }}</v-icon>
                </div>
                <div class="status-text-content">
                  <div class="status-title">{{ item.title }}</div>
                  <div class="status-subtitle">{{ item.subtitle }}</div>
                  <div class="status-description">{{ item.description }}</div>
                </div>
                <v-chip
                  :color="item.status === 'Completed' ? 'green' : 'grey'"
                  text-color="white"
                  small
                  class="status-chip"
                  >{{ item.status }}</v-chip
                >
              </div>
            </div>
          </div>
        </div>
      </div>
    </v-main>
  </v-app>
</template>

<script>
export default {
  name: "OccupancyPermitPage",
  data() {
    return {
      steps: [
        { text: "Fill up the Unified Application Form" },
        { text: "Select Ocompletion Forms" },
        { text: "Download your filled up Forms" },
        { text: "Upload building required documents" },
        { text: "Wait for your application status" },
      ],
      applicationInfo: {
        id: "BP-2025-0808-001",
        submissionDate: "January 15, 2024",
        type: "Full",
        status: "Submitted Application",
        lastUpdated: "2 hours ago",
      },
      statusItems: [
        {
          icon: "mdi-check-circle",
          color: "#ffffff",
          title: "Submitted Application",
          subtitle: "Application ID: BP-2025-0808-001",
          description:
            "Submitted: January 15, 2024. Your application has been successfully submitted and is now in the review process.",
          status: "Completed",
        },
        {
          icon: "mdi-file-document-outline",
          color: "#757575",
          title: "PDF Requirements Checking",
          subtitle: "Application ID: BP-2025-0808-001",
          description:
            "Requirement checking will begin shortly. Your submitted requirements will be reviewed for completeness and accuracy.",
          status: "Not Started",
        },
        {
          icon: "mdi-home-search-outline",
          color: "#757575",
          title: "Building Inspection",
          subtitle: "Application ID: BP-2025-0808-001",
          description:
            "Wait for your onsite inspection schedule once required documents are approved.",
          status: "Not Started",
        },
        {
          icon: "mdi-thumb-up-outline",
          color: "#757575",
          title: "Final Approval",
          subtitle: "Application ID: BP-2025-0808-001",
          description:
            "Final approval and permit issuance will proceed after successful evaluation.",
          status: "Not Started",
        },
      ],
    };
  },
};
</script>

<style scoped>
.page-wrapper {
  background-color: #f4f6f9;
}

/* REMOVED: Styles for the top header */

.main-content-wrapper {
  padding: 24px;
}

.page-header {
  display: flex;
  align-items: center;
  padding: 16px;
  background-color: #ffffff;
  box-shadow: 0 2px 4px rgba(0, 0, 0, 0.05);
  border-radius: 8px;
  margin-bottom: 24px;
}
.page-title {
  font-size: 1.25rem;
  font-weight: 600;
  color: #37474f;
}
.permit-info {
  display: flex;
  flex-direction: column;
  text-align: right;
}
.permit-label {
  font-size: 0.8rem;
  color: #616161;
  font-weight: 500;
}
.permit-id {
  font-size: 0.9rem;
  font-weight: 600;
  color: #2962ff;
}
.sidebar-content {
  background-color: #ffffff;
  padding: 24px;
  display: flex;
  flex-direction: column;
  height: 100%;
}
.guide-title {
  font-size: 1.1rem;
  font-weight: 700;
  color: #212121;
}
.guide-subtitle {
  font-size: 0.9rem;
  color: #616161;
  margin-top: 4px;
}
.stepper-container {
  position: relative;
  padding-left: 20px;
}
.stepper-container::before {
  content: "";
  position: absolute;
  left: 35px;
  top: 15px;
  bottom: 35px;
  width: 2px;
  background-color: #e0e0e0;
  z-index: 1;
}
.step-item {
  display: flex;
  align-items: center;
  margin-bottom: 28px;
  position: relative;
  z-index: 2;
}
.step-circle {
  width: 30px;
  height: 30px;
  border-radius: 50%;
  background-color: #2962ff;
  color: white;
  display: flex;
  align-items: center;
  justify-content: center;
  font-weight: 600;
  font-size: 1rem;
  flex-shrink: 0;
  margin-right: 20px;
}
.step-text {
  font-size: 0.95rem;
  color: #333;
  font-weight: 500;
}
.download-btn {
  text-transform: none;
  font-weight: 600;
  font-size: 1rem;
  border-radius: 8px;
}
.content-panel {
  padding: 0;
}
.logout-btn {
  text-transform: none;
  color: #616161;
  font-weight: 500;
  justify-content: flex-start;
  padding-left: 10px !important;
}
.application-info-card {
  background-color: #ffffff;
  border-radius: 8px !important;
  border: 1px solid #e0e0e0 !important;
  box-shadow: none !important;
  padding: 16px 24px;
}
.info-title {
  font-weight: 600;
  font-size: 1rem;
  color: #212121;
  margin-bottom: 16px;
  display: block;
}
.info-details-grid {
  display: grid;
  grid-template-columns: repeat(auto-fill, minmax(150px, 1fr));
  gap: 16px;
}
.detail-label {
  font-size: 0.8rem;
  color: #757575;
}
.detail-value {
  font-size: 0.9rem;
  color: #212121;
  font-weight: 500;
}
.info-id-right {
  font-size: 0.9rem;
  color: #757575;
  font-weight: 500;
  align-self: flex-start;
  margin-left: 16px;
}
.status-tracker-container {
  background-color: #ffffff;
  border-radius: 8px;
  padding: 24px;
  border: 1px solid #e0e0e0;
}
.tracker-title {
  font-size: 1.1rem;
  font-weight: 700;
  color: #212121;
  margin-bottom: 24px;
}
.status-timeline-container {
  position: relative;
  padding-left: 25px;
}
.status-timeline-container::before {
  content: "";
  position: absolute;
  left: 44px;
  top: 25px;
  bottom: 25px;
  width: 2px;
  background-color: #e0e0e0;
  z-index: 1;
}
.status-item {
  display: flex;
  align-items: flex-start;
  position: relative;
  z-index: 2;
  margin-bottom: 24px;
}
.status-item:last-child {
  margin-bottom: 0;
}
.status-icon-wrapper {
  width: 40px;
  height: 40px;
  border-radius: 50%;
  display: flex;
  align-items: center;
  justify-content: center;
  flex-shrink: 0;
  margin-right: 20px;
  border: 4px solid #f4f6f9;
}
.status-icon-wrapper.completed {
  background-color: #4caf50;
}
.status-icon-wrapper.not-started {
  background-color: #bdbdbd;
}
.status-icon-wrapper .v-icon {
  font-size: 20px;
}
.status-text-content {
  flex-grow: 1;
}
.status-title {
  font-weight: 600;
  font-size: 1rem;
  color: #333;
}
.status-subtitle {
  font-size: 0.85rem;
  color: #757575;
  margin-top: 2px;
}
.status-description {
  font-size: 0.9rem;
  color: #616161;
  margin-top: 4px;
  max-width: 90%;
}
.status-chip {
  font-weight: 500;
  margin-left: 16px;
  height: 24px !important;
}
</style>
