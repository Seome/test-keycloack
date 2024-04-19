<template>
  <div>
    <button @click="getLogin">Get Login</button>
    <h1>Add User to Keycloak</h1>
    <form @submit.prevent="addUser">
      <label for="username">Username:</label>
      <input type="text" id="username" v-model="user.username" required />
      <label for="email">Email:</label>
      <input type="email" id="email" v-model="user.email" required />
      <label for="password">Password:</label>
      <input type="password" id="password" v-model="user.password" required />
      <button type="submit">Add User</button>
    </form>
    <p v-if="message">{{ message }}</p>
  </div>
</template>

<script>
import axios from 'axios';

export default {
  data() {
    return {
      user: {
        username: '',
        email: '',
        password: '',
      },
      message: '',
    };
  },
  methods: {
    async addUser() {
      try {
        const userPayload = {
          attributes: {
            attribute_key: 'test_value',
          },
          credentials: [
            {
              temporary: false,
              type: 'password',
              value: this.user.password,
            },
          ],
          username: this.user.username,
          firstName: 'Test',
          lastName: 'Admin',
          email: this.user.email,
          emailVerified: false,
          enabled: true,
        };

        const response = await axios.post(
          'http://localhost:8080/admin/realms/test/users',
          userPayload,
          {
            headers: {
              'Content-Type': 'application/json',
              Authorization: 'eyJhbGciOiJSUzI1NiIsInR5cCIgOiAiSldUIiwia2lkIiA6ICJfRF9ONjNWeE1XUWNLblFsUHBrZzdyWVRXWDRsdFRlZE0wYzBvUXVxVlpzIn0.eyJleHAiOjE3MTM1MzE1MTEsImlhdCI6MTcxMzUzMTIxMSwianRpIjoiN2QwYzY0MzItMDFmMC00MGZhLWI1MWItODMyODNhOThkZjljIiwiaXNzIjoiaHR0cDovL2xvY2FsaG9zdDo4MDgwL3JlYWxtcy90ZXN0IiwiYXVkIjpbInJlYWxtLW1hbmFnZW1lbnQiLCJhY2NvdW50Il0sInN1YiI6IjhmYTZmYjM0LTBiOTYtNDZkOC1hNDdmLTM5NjZmYjYwNzE3MiIsInR5cCI6IkJlYXJlciIsImF6cCI6InRlc3QiLCJhY3IiOiIxIiwiYWxsb3dlZC1vcmlnaW5zIjpbIi8qIiwiaHR0cDovL2xvY2FsaG9zdDo4MDgxLyJdLCJyZWFsbV9hY2Nlc3MiOnsicm9sZXMiOlsiZGVmYXVsdC1yb2xlcy10ZXN0Iiwib2ZmbGluZV9hY2Nlc3MiLCJ1bWFfYXV0aG9yaXphdGlvbiJdfSwicmVzb3VyY2VfYWNjZXNzIjp7InJlYWxtLW1hbmFnZW1lbnQiOnsicm9sZXMiOlsidmlldy1yZWFsbSIsInZpZXctaWRlbnRpdHktcHJvdmlkZXJzIiwibWFuYWdlLWlkZW50aXR5LXByb3ZpZGVycyIsImltcGVyc29uYXRpb24iLCJyZWFsbS1hZG1pbiIsImNyZWF0ZS1jbGllbnQiLCJtYW5hZ2UtdXNlcnMiLCJxdWVyeS1yZWFsbXMiLCJ2aWV3LWF1dGhvcml6YXRpb24iLCJxdWVyeS1jbGllbnRzIiwicXVlcnktdXNlcnMiLCJtYW5hZ2UtZXZlbnRzIiwibWFuYWdlLXJlYWxtIiwidmlldy1ldmVudHMiLCJ2aWV3LXVzZXJzIiwidmlldy1jbGllbnRzIiwibWFuYWdlLWF1dGhvcml6YXRpb24iLCJtYW5hZ2UtY2xpZW50cyIsInF1ZXJ5LWdyb3VwcyJdfSwidGVzdCI6eyJyb2xlcyI6WyJ1bWFfcHJvdGVjdGlvbiJdfSwiYWNjb3VudCI6eyJyb2xlcyI6WyJtYW5hZ2UtYWNjb3VudCIsIm1hbmFnZS1hY2NvdW50LWxpbmtzIiwidmlldy1wcm9maWxlIl19fSwic2NvcGUiOiJlbWFpbCBwcm9maWxlIiwiZW1haWxfdmVyaWZpZWQiOmZhbHNlLCJjbGllbnRIb3N0IjoiMTcyLjE3LjAuMSIsInByZWZlcnJlZF91c2VybmFtZSI6InNlcnZpY2UtYWNjb3VudC10ZXN0IiwiY2xpZW50QWRkcmVzcyI6IjE3Mi4xNy4wLjEiLCJjbGllbnRfaWQiOiJ0ZXN0In0.Y__gMko4m6A4GBBj9kTPN6euRCV9-RUXZQIbX8Guq9YurAMfcJamUgbM51hfbnMpqGgc7FMuf9JWp8nS0-0PN4sgpQZvmm3_CODzWvZsAdsITwZ3tMM5Su71dSdhO92FYwyRKX5ToHKYjWwTMRJLFvmurHUEb8HmCalQuUrJd06QS4Rq9I8tAf3cHPViSIX5jev5JubOtKyxJd3eOwxh3diwrKA0LAWk9z06ZuRchd-rTU3K4_CfX1E2_KMXOD-Y-h4aGaWxkYeGK-Jvd85yEv8lrvdE7TVJ73aA0BEp7fJNZBfBvsCwRnOt09XtlFURWawV3nyXS6tiRbCUK78ijA',
            },
          }
        );

        this.message = 'User added successfully!';
        console.log(response.data);
      } catch (error) {
        this.message = 'Error adding user.';
        console.error(error);
      }
    },
    async getLogin() {
      try {
        const userPayload = {
          grant_type: "client_credentials",
          client_id: "test",
          client_secret: "v0SoGqXxHAwgN2VKg1eDfbdvnu3Tzkz3"
        };

        const response = await axios.post(
          'http://localhost:8080/admin/realms/test/protocol/openid-connect/token',
          userPayload,
          {
            headers: {
              'Content-Type': 'application/json',
            },
          }
        );

        this.message = 'User added successfully!';
        console.log(response.data);
      } catch (error) {
        this.message = 'Error adding user.';
        console.error(error);
      }
    },
    
  },
};
</script>
