<template>
  <div class="page-content">
    <section class="pricing">
      <div class="pricing--container">
        <div class="pricing--leader">
          <h1 class="pricing--title">Developer Friendly Pricing</h1>
          <p class="pricing--subtitle">Whether you're building a new application or scaling to millions of users, our plans have you covered.</p>
        </div>
      </div>
      <div class="pricing--background-curve">
        <img src="/img/curve-doubleLeft.png" />
      </div>
      <div class="pricing-alt-bg">
        <div class="pricing--container">
          <div class="pricing--costs">
            <div class="pricing-section pricing-card-intro">
              <div class="pricing-card">
                <div class="pricing-card-column">
                  <h3>Add Auth in minutes (with no credit card)</h3>
                  <div class="pricing-card-price">
                      <p class="pricing-card-amount">
                        $0
                      </p>
                      <p class="pricing-card-detail">
                        per month
                      </p>
                  </div>
                  <p class="pricing-card-subtitle">
                    Up to 1,000 monthly active users
                  </p>
                  <a :href="$page.frontmatter.links.signup" class="Button--red">
                    Get Started Free
                  </a>
                </div>
                <div class="pricing-card-column">
                  <h4>Identity and access control for your app</h4>
                  <div class="pricing-card-lists">
                    <ul class="pricing--icon-list">
                      <li>Authentication</li>
                      <li>Authorization</li>
                      <li>Basic multi-factor authentication</li>
                    </ul>
                    <ul class="pricing--icon-list">
                      <li>User management</li>
                      <li>Email support</li>
                      <li>Customizable sign-in and registration</li>
                    </ul>
                  </div>
                </div>
              </div>
            </div>
          </div>
        </div>
        <div class="pricing--container">
          <div class="pricing--editions">
            <div class="pricing-section">
              <div class="pricing-card pricing-card-table">
                <div class="pricing-card-row pricing-card-header">
                  <div class="pricing-card-column desktop">
                    <h3 class="pricing-card-table-name">Editions</h3>
                  </div>
                  <template v-for="(edition, index) in $page.frontmatter.editions">
                    <div class="pricing-card-column" v-bind:key="edition.name">
                      <div class="pricing-card-column-header">
                        <h4>{{edition.name}}</h4>
                        <template v-if="index === 0">
                          <p>Priced at</p>
                          <p class="pricing-card-price">{{mauPrice}}</p>
                          <p>per month for up to</p>
                          <select v-model="mauPrice">
                            <option v-for="(price, index) in $page.frontmatter.pricing" :value="price.price" :key="index">
                              {{price.maus}}
                            </option>
                          </select>
                          <a :href="$page.frontmatter.links.signup" class="Button--red">Start Free</a>
                        </template>
                        <template v-else>
                          <p>{{edition.subheading}}</p>
                          <a :href="$page.frontmatter.links.contactSales" class="Button--whiteOutline">Contact Us</a>
                        </template>
                      </div>
                      <template v-for="(details, feature) in $page.frontmatter.features">
                        <div class="pricing-card-row mobile" v-bind:key="details.name">
                          <div class="pricing-card-column">
                            {{details.name}}
                            <ul v-if="details.bullets">
                              <li v-for="(bullet, bulletIndex) in details.bullets" v-bind:key="bulletIndex">
                                {{bullet}}
                              </li>
                            </ul>
                          </div>
                          <div class="pricing-card-column" v-if="typeof edition[feature] === 'object'">
                              <img src="/img/icons/icon--check.svg" v-if="edition[feature].enabled" class="pricing-card-check" />
                              {{edition[feature].additionalNote}}
                          </div>
                          <div class="pricing-card-column" v-else>
                            <img src="/img/icons/icon--check.svg" v-if="edition[feature]" class="pricing-card-check" />
                          </div>
                        </div>
                      </template>
                    </div>
                  </template>
                </div>
                <template v-for="(details, feature) in $page.frontmatter.features">
                  <div class="pricing-card-row desktop" v-bind:key="details.name">
                    <div class="pricing-card-column">
                      {{details.name}}
                      <ul v-if="details.bullets">
                        <li v-for="(bullet, bulletIndex) in details.bullets" v-bind:key="bulletIndex">
                          {{bullet}}
                        </li>
                      </ul>
                    </div>
                    <template v-for="edition in $page.frontmatter.editions">
                      <div class="pricing-card-column" v-if="typeof edition[feature] === 'object'" v-bind:key="edition.name">
                        <div>
                          <img src="/img/icons/icon--check.svg" v-if="edition[feature].enabled" />
                          {{edition[feature].additionalNote}}
                        </div>
                      </div>
                      <div class="pricing-card-column" v-else v-bind:key="edition.name">
                        <img src="/img/icons/icon--check.svg" v-if="edition[feature]" />
                      </div>
                    </template>
                  </div>
                </template>
              </div>
            </div>
          </div>
        </div>
        <div class="pricing--container">
          <div class="pricing--addons">
            <div class="pricing-addons-header">
              <h1>Add-Ons</h1>
              <h4>
                Learn more about add-on products at <a :href="$page.frontmatter.links.pricing">okta.com/pricing</a>
              </h4>
            </div>
            <div class="pricing-addons-tiles">
              <template v-for="addon in $page.frontmatter.addons">
                <a class="pricing-addons-tile" target="_blank" rel="noopener noreferrer" :href="addon.link" v-bind:key="addon.title">
                  <img :src="addon.icon" />
                  <p>{{addon.title}}</p>
                </a>
              </template>
            </div>
          </div>
        </div>
      </div>
      <div class="pricing--background-curve">
        <img src="/img/curve-singleRightLight.png" />
      </div>
      <div class="pricing--container">
        <div class="pricing--faq">
          <h1>Frequently asked questions</h1>
          <template v-for="(item, index) in $page.frontmatter.faqs">
            <div class="pricing-faq-item" v-bind:class="{ 'is-active': faqShownStates[index] }" v-bind:key="index">
              <button class="pricing-faq-item-title" v-on:click="toggleFaqShown(index)">
                {{item.title}}
              </button>
              <div class="pricing-faq-item-content" v-html="item.content"></div>
            </div>
          </template>
        </div>
      </div>
      <div class="pricing--container">
        <div class="pricing--questions">
          <h2>More questions?</h2>
          <p>
            We'd love to hear them. A real, technical human will get back to you shortly.
          </p>
          <a :href="$page.frontmatter.links.emailSupport" class="Button--red">
            Email Support
          </a>
        </div>
      </div>
      <div class="pricing--background-curve">
        <img src="/img/curve-doubleLeft.png" />
      </div>
      <div class="pricing--footer">
        <h1>Trusted by developers</h1>
        <div class="pricing--footer--logos">
          <img src="/img/logos/logo--adobe.png" />
          <img src="/img/logos/logo--pitney.png" />
          <img src="/img/logos/logo--experian.png" />
          <img src="/img/logos/logo--advent.png" />
        </div>
      </div>
    </section>
  </div>
</template>

<script>
export default {
  data: () => ({
    faqShownStates: [
      false,
      false,
      false,
    ],
    mauPrice: '$0',
  }),
  methods: {
    toggleFaqShown(faqIndex) {
      this.$set(this.faqShownStates, faqIndex, !this.faqShownStates[faqIndex]);
    }
  }
}
</script>
