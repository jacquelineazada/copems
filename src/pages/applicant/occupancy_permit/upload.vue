<template>
  <div class="page-wrapper">
    <v-container fluid class="main-content" style="max-width: 1200px">
      <div class="header-section">
        <h1>Supporting Documents</h1>
        <p>Please upload the required documents to proceed with your application</p>
      </div>

      <v-row>
        <!-- Construction Logbook Uploader -->
        <v-col cols="12" md="4">
          <div class="upload-box">
            <div class="upload-title">
              <v-icon color="red" left small>mdi-file-document</v-icon>
              Construction Logbook *
            </div>
            <div class="upload-caption">
              This document must be signed by the contractor and the supervising
              professional as proof of actual construction activities.
            </div>
            <v-card outlined class="file-drop-area" @click="triggerFileUpload('logbook')">
              <v-icon size="48" color="grey lighten-1">mdi-cloud-upload-outline</v-icon>
              <div class="file-drop-text">Drop files here or click to browse</div>
              <div class="file-type-hint">PDF</div>
              <input
                type="file"
                ref="logbook"
                @change="handleFileUpload($event, 'logbook')"
                hidden
              />
            </v-card>
            <div v-if="files.logbook" class="file-name-chip">
              {{ files.logbook.name }}
            </div>
          </div>
        </v-col>

        <!-- As-built Plans Uploader -->
        <v-col cols="12" md="4">
          <div class="upload-box">
            <div class="upload-title">
              <v-icon color="red" left small>mdi-file-document</v-icon>
              As-built Plans
            </div>
            <div class="upload-caption">
              Required only for projects with major changes or deviations from the
              approved building plans.
            </div>
            <v-card outlined class="file-drop-area" @click="triggerFileUpload('plans')">
              <v-icon size="48" color="grey lighten-1">mdi-cloud-upload-outline</v-icon>
              <div class="file-drop-text">Drop files here or click to browse</div>
              <div class="file-type-hint">PDF</div>
              <input
                type="file"
                ref="plans"
                @change="handleFileUpload($event, 'plans')"
                hidden
              />
            </v-card>
            <div v-if="files.plans" class="file-name-chip">
              {{ files.plans.name }}
            </div>
          </div>
        </v-col>

        <!-- Sketch of Location Uploader -->
        <v-col cols="12" md="4">
          <div class="upload-box">
            <div class="upload-title">
              <v-icon color="red" left small>mdi-file-document</v-icon>
              Sketch of Location
            </div>
            <div class="upload-caption">
              A simple drawing showing the project's location, nearby streets, and major
              landmarks.
            </div>
            <v-card outlined class="file-drop-area" @click="triggerFileUpload('sketch')">
              <v-icon size="48" color="grey lighten-1">mdi-cloud-upload-outline</v-icon>
              <div class="file-drop-text">Drop files here or click to browse</div>
              <div class="file-type-hint">PDF</div>
              <input
                type="file"
                ref="sketch"
                @change="handleFileUpload($event, 'sketch')"
                hidden
              />
            </v-card>
            <div v-if="files.sketch" class="file-name-chip">
              {{ files.sketch.name }}
            </div>
          </div>
        </v-col>
      </v-row>

      <div class="submit-section">
        <v-btn color="primary" large @click="submitDocuments"> Submit </v-btn>
      </div>
    </v-container>

    <!-- ++ Success Dialog (Pop-up) ++ -->
    <v-dialog v-model="dialog" persistent max-width="550px">
      <v-card class="dialog-card">
        <v-btn icon class="close-button" @click="closeDialog">
          <v-icon>mdi-close</v-icon>
        </v-btn>
        <v-card-text class="text-center">
          <div class="icon-container-success">
            <v-icon size="40" color="white">mdi-check</v-icon>
          </div>
          <h2 class="dialog-title">Application Submitted Successfully</h2>
          <p class="dialog-description">
            Your occupancy permit application has been submitted successfully. It will now
            go through our verification process, followed by plan evaluation, before the
            final permit release.
          </p>

          <div class="status-section">
            <div class="status-header">
              <span>Application Status</span>
              <span class="status-tag">Under Review</span>
            </div>
            <div class="status-progress-bar">
              <div class="progress-step active">Submitted</div>
              <div class="progress-step">Checking</div>
              <div class="progress-step">Inspection</div>
              <div class="progress-step">Release</div>
            </div>
          </div>

          <div class="info-box">
            <div class="info-box-title">
              <v-icon color="primary" left>mdi-information-outline</v-icon>
              Application Process
            </div>
            <p>
              Your application will go through three main stages: verification of uploaded
              plans, evaluation of verified plans, and final permit release. Each stage
              will be reviewed by our technical team.
            </p>
          </div>

          <div class="reference-section">
            <span>Reference Number:</span>
            <strong>{{ referenceNumber }}</strong>
          </div>
        </v-card-text>
        <v-card-actions class="dialog-actions">
          <v-btn color="primary" block large @click="closeDialog" to="/StatusOne">
            Back to home
          </v-btn>
          <div class="footer-note">
            You can track your application status in your dashboard or contact support if
            you have any questions.
          </div>
        </v-card-actions>
      </v-card>
    </v-dialog>
  </div>
</template>

<script>
export default {
  name: "SupportingDocuments",
  data() {
    return {
      dialog: false, // Controls the visibility of the pop-up
      referenceNumber: null,
      files: {
        logbook: null,
        plans: null,
        sketch: null,
      },
    };
  },
  methods: {
    triggerFileUpload(fileRef) {
      this.$refs[fileRef].click();
    },
    handleFileUpload(event, fileType) {
      const file = event.target.files[0];
      if (file) {
        this.files[fileType] = file;
        console.log(`File selected for ${fileType}:`, file.name);
      }
    },
    submitDocuments() {
      if (!this.files.logbook) {
        alert("Construction Logbook is a required document.");
        return;
      }

      // Generate a random reference number
      const randomPart = Math.floor(1000 + Math.random() * 9000);
      this.referenceNumber = `#BP-2023-00${randomPart}`;

      console.log("Submitting documents:", this.files);
      this.dialog = true; // Show the pop-up
    },
    closeDialog() {
      this.dialog = false; // Close the pop-up
      // Optionally, you can reset the form here
    },
  },
};
</script>

<style scoped>
/* --- Main Page Styles --- */
.page-wrapper {
  background-color: #f4f6f9;
  min-height: 100vh;
  padding-top: 60px;
}
.main-content {
  padding-top: 40px;
  padding-bottom: 60px;
}
.header-section {
  text-align: center;
  margin-bottom: 50px;
}
.header-section h1 {
  font-size: 2.25rem;
  font-weight: 700;
  color: #333;
  margin-bottom: 12px;
}
.header-section p {
  font-size: 1.1rem;
  color: #6c757d;
  line-height: 1.6;
  max-width: 600px;
  margin: 0 auto;
}
.upload-box {
  margin-bottom: 20px;
}
.upload-title {
  font-size: 1.1rem;
  font-weight: 600;
  color: #333;
  margin-bottom: 8px;
  text-align: left;
}
.upload-caption {
  font-size: 0.9rem;
  color: #6c757d;
  line-height: 1.5;
  margin-bottom: 16px;
  min-height: 65px;
  text-align: left;
}
.file-drop-area {
  border: 2px dashed #dce4e8;
  border-radius: 8px;
  padding: 40px 20px;
  text-align: center;
  cursor: pointer;
  transition: background-color 0.3s ease;
  background-color: #ffffff;
}
.file-drop-area:hover {
  background-color: #f8fafc;
}
.file-drop-text {
  margin-top: 12px;
  color: #555;
  font-weight: 500;
}
.file-type-hint {
  font-size: 0.8rem;
  color: #aaa;
  margin-top: 4px;
}
.file-name-chip {
  background-color: #e3f2fd;
  color: #1976d2;
  padding: 4px 12px;
  border-radius: 16px;
  font-size: 0.85rem;
  margin-top: 12px;
  display: inline-block;
  text-align: left;
}
.submit-section {
  text-align: right;
  margin-top: 40px;
}

/* --- Dialog (Pop-up) Styles --- */
.dialog-card {
  padding: 28px;
  border-radius: 12px !important;
}
.close-button {
  position: absolute;
  top: 19px;
  right: 16px;
}
.icon-container-success {
  width: 60px;
  height: 60px;
  border-radius: 50%;
  background-color: #4caf50; /* Green success color */
  display: flex;
  align-items: center;
  justify-content: center;
  margin: 0 auto 20px auto;
}
.dialog-title {
  font-size: 1.5rem;
  font-weight: 700;
  color: #333;
  margin-bottom: 12px;
}
.dialog-description {
  font-size: 1rem;
  color: #6c757d;
  line-height: 1.6;
  margin-bottom: 24px;
}
.status-section {
  margin-bottom: 24px;
}
.status-header {
  display: flex;
  justify-content: space-between;
  align-items: center;
  margin-bottom: 12px;
  font-weight: 600;
}
.status-tag {
  background-color: #e3f2fd;
  color: #1e88e5;
  padding: 4px 10px;
  border-radius: 19px;
  font-size: 0.8rem;
}
.status-progress-bar {
  display: flex;
  position: relative;
  background-color: #e0e0e0;
  height: 4px;
  border-radius: 2px;
  margin: 0 8px; /* Add margin to prevent text touching edges */
}
.status-progress-bar::before {
  content: "";
  position: absolute;
  left: 0;
  top: 0;
  height: 100%;
  width: 12.5%; /* Covers the first half of the first step */
  background-color: #4caf50;
  border-radius: 2px;
}
.progress-step {
  font-size: 0.8rem;
  color: #757575;
  position: relative;
  width: 26%;
  padding-top: 29px;
  white-space: nowrap; /* Prevent text from wrapping */
}
/* ++ Fixes start here ++ */
.progress-step:first-child {
  text-align: left;
}
.progress-step:last-child {
  text-align: right;
}
.progress-step:nth-child(2) {
  text-align: center;
  transform: translateX(-15%); /* Adjust position of 2nd item */
}
.progress-step:nth-child(3) {
  text-align: center;
  transform: translateX(15%); /* Adjust position of 3rd item */
}
/* ++ Fixes end here ++ */

.progress-step::before {
  content: "";
  position: absolute;
  top: -6px;
  left: 50%;
  transform: translateX(-50%);
  width: 16px;
  height: 16px;
  border-radius: 50%;
  background-color: #e0e0e0;
  border: 2px solid #f4f6f9;
}

/* Marker alignment for first and last child */
.progress-step:first-child::before {
  left: 0;
  transform: none;
}
.progress-step:last-child::before {
  left: auto;
  right: 0;
  transform: none;
}
.progress-step.active {
  color: #4caf50;
  font-weight: 600;
}
.progress-step.active::before {
  background-color: #4caf50;
}
.info-box {
  background-color: #e3f2fd;
  border-radius: 8px;
  padding: 16px;
  text-align: left;
  margin-bottom: 24px;
}
.info-box-title {
  font-weight: 600;
  color: #1e88e5;
  margin-bottom: 8px;
  display: flex;
  align-items: center;
}
.info-box p {
  font-size: 0.9rem;
  color: #424242;
  line-height: 1.5;
  margin-bottom: 0;
}
.reference-section {
  background-color: #f5f5f5;
  padding: 12px;
  border-radius: 8px;
  font-size: 1rem;
  display: flex;
  justify-content: space-between;
  align-items: center;
}
.dialog-actions {
  padding: 0 24px 24px 24px !important;
  flex-direction: column;
}
.footer-note {
  font-size: 0.85rem;
  color: #757575;
  margin-top: 16px;
  text-align: center;
}
.v-btn {
  text-transform: none;
  font-weight: 600;
  font-size: 1rem;
  border-radius: 8px;
  box-shadow: none;
}
</style>
