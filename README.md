- 👋 Hi, I’m @kishore010602
- 👀 I’m interested in ...
- 🌱 I’m currently learning ...
- 💞️ I’m looking to collaborate on ...
- 📫 How to reach me ...
- 😄 Pronouns: ...
- ⚡ Fun fact: ...

<!---
kishore010602/kishore010602 is a ✨ special ✨ repository because its `README.md` (this file) appears on your GitHub profile.
You can click the Preview link to take a look at your changes.
--->
  try {
            donorService.createDonorProfile(donor);
            Donor loggedInDonor = donorService.loginDonorProfile(donor.getEmail(), donor.getPassword());
            assertNotNull(loggedInDonor);
            assertEquals(donor.getName(), loggedInDonor.getName());
            assertEquals(donor.getEmail(), loggedInDonor.getEmail());
            assertEquals(donor.getPassword(), loggedInDonor.getPassword());
        } catch (DonorExceptions e) {
            fail("Exception thrown while logging in donor profile: " + e.getMessage());
        }
    }
@Test
    void updateDonorNameByIdTest() {
        Donor donor = new Donor("John", "john@example.com", "password");
        donor = donorRepositoryDao.save(donor);

        String newName = "John Doe";
        try {
            Donor updatedDonor = donorService.updateDonorNameById(donor.getId(), newName);
            assertEquals(newName, updatedDonor.getName());

            Optional<Donor> optionalDonor = donorRepositoryDao.findById(donor.getId());
            assertTrue(optionalDonor.isPresent());
            assertEquals(newName, optionalDonor.get().getName());
        } catch (DonorExceptions e) {
            fail("Exception thrown while updating donor's name: " + e.getMessage());
        }
    }

    @Test
    void deleteDonorByIdTest() {
        Donor donor = new Donor("Jane", "jane@example.com", "password");
        donor = donorRepositoryDao.save(donor);

        try {
            String result = donorService.deleteDonorById(donor.getId());
            assertEquals("Profile deleted successfully!!", result);

            Optional<Donor> optionalDonor = donorRepositoryDao.findById(donor.getId());
            assertFalse(optionalDonor.isPresent());
        } catch (DonorExceptions e) {
            fail("Exception thrown while deleting donor profile: " + e.getMessage());
        }
    }
