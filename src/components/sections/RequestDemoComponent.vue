<template>
    <section id="demo" class="section-demo">
        <div class="container">
            <div class="demo-grid">
                <div class="demo-copy">
                    <div class="section-header left">
                        <span class="section-tag">Get in Touch</span>
                        <h2 class="section-title">See the Ruffian EMP 270G in Action</h2>
                        <p class="section-desc">
                            Our team can arrange an on-site demo, connect you with a local distributor, or answer technical questions directly.
                        </p>
                    </div>
                    <ul class="demo-bullets">
                        <li class="demo-bullet">
                            <span class="demo-bullet-icon">✓</span>
                            Live product demonstration at your job site
                        </li>
                        <li class="demo-bullet">
                            <span class="demo-bullet-icon">✓</span>
                            Technical consultation with a welding specialist
                        </li>
                        <li class="demo-bullet">
                            <span class="demo-bullet-icon">✓</span>
                            Custom quote for fleet or volume orders
                        </li>
                        <li class="demo-bullet">
                            <span class="demo-bullet-icon">✓</span>
                            Find your nearest authorized ESAB distributor
                        </li>
                    </ul>
                </div>
                <div class="demo-form-wrap">
                    <h3>Request a Demo</h3>
                    <p class="form-subtitle">An ESAB rep will contact you within one business day.</p>
                    <form  @submit.prevent="submitDemoRequest">
                        <div class="form-row">
                            <div class="form-group">
                            <label class="form-label">First Name <span class="required">*</span></label>
                            <input type="text" v-model="form.firstName" class="form-input" placeholder="John">
                            <p v-if="errors.firstName" class="form-error-msg"> {{ errors.firstName }}</p>
                            </div>
                            <div class="form-group">
                            <label class="form-label">Last Name <span class="required">*</span></label>
                            <input type="text" v-model="form.lastName" class="form-input" placeholder="Smith">
                            <p v-if="errors.lastName" class="form-error-msg"> {{ errors.lastName }}</p>
                            </div>
                        </div>

                        <div class="form-group">
                            <label class="form-label">Work Email <span class="required">*</span></label>
                            <input type="email" v-model="form.email" class="form-input" placeholder="john.smith@company.com">
                            <p v-if="errors.email" class="form-error-msg"> {{ errors.email }}</p>
                        </div>

                        <div class="form-group">
                            <label class="form-label">Company / Organization <span class="required">*</span></label>
                            <input type="text" v-model="form.company" class="form-input" placeholder="Acme Welding Co.">
                            <p v-if="errors.company" class="form-error-msg"> {{ errors.company }}</p>
                        </div>

                        <div class="form-group">
                            <label class="form-label">Phone Number</label>
                            <input type="tel" v-model="form.phone" class="form-input" placeholder="+1 (555) 000-0000">
                        </div>

                        <div class="form-group">
                            <label class="form-label">What are you interested in?</label>
                            <DropdownComponent v-model="form.interest" :options="interests" placeholder="Select an option"/>
                        </div>

                        <p class="form-privacy">
                            By submitting this form you agree to ESAB's
                            <a href="#">Privacy Policy</a> and consent to being
                            contacted by an ESAB representative.
                        </p>

                        <button class="btn-submit" type="submit">Submit Request</button>
                    </form>
                </div>
            </div>
        </div>
    </section>
</template>
<script setup>
import { ref } from 'vue';
import DropdownComponent from '../shared/DropdownComponent.vue';

const interests = [
  { label: 'On-site product demonstration', value: 'On-site product demonstration' },
  { label: 'Technical consultation', value: 'Technical consultation' },
  { label: 'Distributor referral', value: 'Distributor referral' },
  { label: 'Volume / fleet pricing', value: 'Volume / fleet pricing' },
  { label: 'Technical specifications', value: 'Technical specifications' },
  { label: 'General inquiry', value: 'General inquiry' }
]

const form = ref({
  firstName: '',
  lastName: '',
  email: '',
  company: '',
  phone: '',
  interest: ''
})

const errors = ref({})

const validate = () => {
  errors.value = {}

  if (!form.value.firstName) {
    errors.value.firstName = 'First name is required'
  }

  if (!form.value.lastName) {
    errors.value.lastName = 'Last name is required'
  }

  if (!form.value.email) {
    errors.value.email = 'Email is required'
  } else if (!/^\S+@\S+\.\S+$/.test(form.value.email)) {
    errors.value.email = 'Invalid email'
  }

  if (!form.value.company) {
    errors.value.company = 'Company is required'
  }

  return Object.keys(errors.value).length === 0
}

const submitDemoRequest = () => {
    if(validate()) {
        console.log('Demo request submitted:', form.value)
        alert('Demo request submitted! An ESAB representative will contact you soon.');
    }
};
</script>
<style scoped lang="scss">
@use '../../styles/_variables' as *;
.demo-grid{
    display: grid;
    grid-template-columns: 1fr 1fr;
    gap: $sp-8;
    align-items: start;
}
@media (max-width: 1024px) {
    .demo-grid {
        grid-template-columns: 1fr;
    }
}
.section-header.left {
    text-align: left;
    margin: 0 0 $sp-4;
}
.section-tag {
    background: rgba($esab-white, 0.06);
    border-color: rgba($esab-white, 0.12);
    color: rgba($esab-white, 0.5);
}
.section-title {
    color: $esab-white;
    font-size: 28px;
}
.section-desc {
    color: rgba($esab-white, 0.6);
    margin-bottom: $sp-5;
}
.demo-bullets {
    display: flex;
    flex-direction: column;
    gap: $sp-2;
}
.demo-bullet{
    display: flex;
    align-items: center;
    gap: $sp-2;
    font-size: $ft-16;
    font-weight: $fw-medium;
    color: rgba($esab-white, 0.85);
}
.demo-bullet-icon {
    width: $sp-3;
    height: $sp-3;
    border-radius: 50%;
    background: $esab-yellow;
    color: $esab-black;
    font-size: 13px;
    font-weight: $fw-bolder;
    display: flex;
    align-items: center;
    justify-content: center;
    flex-shrink: 0;
}
.demo-form-wrap {
    background: $esab-white;
    border-radius: $radius-lg;
    padding: $sp-6 $sp-5;
    color: $text;
    h3 {
        font-size: $sp-3;
        font-weight: $fw-bold;
        line-height: 1.1;
        margin-bottom: 4px;
        color: $text;
    }
    .form-subtitle {
        font-size: $ft-14;
        color: $text-muted;
        line-height: 1.4;
        margin-bottom: $sp-4;
    }
}
.form-row {
    display: grid;
    grid-template-columns: 1fr 1fr;
    gap: $sp-2;
}
.form-group {
    display: flex;
    flex-direction: column;
    gap: 4px;
    margin-bottom: $sp-2;
}
.form-label {
    font-size: $ft-14;
    font-weight: $fw-bold;
    color: $text;
}
.form-input {
    min-height: 44px;
    padding: 0 $sp-2;
    border: 1px solid $esab-gray-4;
    border-radius: $radius;
    font-size: $ft-16;
    color: $text;
    background: $esab-white;
    transition: border-color 0.2s;
    width: 100%;
    &:focus-visible {
        border-color: $esab-info;
        outline: none;
    }
}
.form-select {
    min-height: 44px;
    padding: 0 $sp-2;
    border: 1px solid $esab-gray-4;
    border-radius: $radius;
    font-size: $ft-16;
    color: $text;
    background: $esab-white;
    width: 100%;
    appearance: none;
    background-repeat: no-repeat;
    background-position: right 14px center;
    cursor: pointer;
    &:focus-visible {
        border-color: $esab-info;
        outline: none;
    }
}

.form-privacy {
    font-size: $ft-12;
    color: $text-muted;
    line-height: 1.63;
    margin-bottom: $sp-3;
    a {
        color: $esab-blue;
        text-decoration: underline;
    }
}
.btn-submit {
    width: 100%;
    height: 50px;
    background: $esab-yellow;
    color: $esab-black;
    border: none;
    border-radius: $radius;
    font-size: $ft-16;
    font-weight: $fw-bold;
    text-transform: uppercase;
    letter-spacing: 0.03em;
    cursor: pointer;
    transition: background 0.2s;

    &:hover {
        background: #e6d100;
    }
}
.form-label .required {
    color: $esab-error;
    margin-left: 2px;
}
.form-error-msg {
    color: $esab-error;
    font-size: $ft-12;
    margin-top: 4px;
}
</style>