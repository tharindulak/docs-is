---
title: Index backup
mkdocs_template: landing-page
deployment_options:
  - Self-hosted
custom_edit_url: https://github.com/wso2/docs-is/edit/master/en/identity-server/6.0.0/docs/index-backup.md
---

<div>
   <div className="container-fluid px-lg-5 py-5">
      <div className="row pt-3">
         <div className="col-xl-1"></div>
         <div className="col-xl-6 col-lg-7 col-md-12">
            <h1 className="iam-heading-text">New to Identity Server?</h1>
            <p className="iam-sub-text">
               Identity Server is all about simplifying the Identity and Access Management (IAM) needs of your organization. It is based on open standards and is fully open source. 
               <a className="read-more-link" href="get-started/overview/">
                  <b>Read more</b><i className="material-icons md-36 read-more-arrow">arrow_right_alt</i>
               </a>
            </p>
            <div className="btn-row">
               <a className="get-started-btn mb-2" href="deploy/get-started/run-the-product/">Get Started</a>
               <a className="download-btn mb-2" href="https://wso2.com/identity-and-access-management/">Download</a>
            </div>
         </div>
         <div className="col-xl-2 col-lg-1"></div>
         
         <div className="col-xl-2 col-lg-4 col-md-12 d-none d-lg-block">
            <ul className="hot-links-list">
               <li><a className="hot-links-text" href="https://wso2is.slack.com/">Slack</a></li>
               <li><a className="hot-links-text" href="get-started/community/">Community</a></li>
               <li><a className="hot-links-text" href="https://wso2.com/blog/identity-and-access-management/">Blogs/Articles</a></li>
               <li><a className="hot-links-text" href="deploy/environment-compatibility/">Compatibility</a></li>
               <li><a className="hot-links-text" href="https://wso2.com/training/identity-server-fundamentals">Training</a></li>
               <li><a className="hot-links-text" href="https://store.wso2.com/store/assets/isconnector/list">Connectors</a></li>
               <li><a className="hot-links-text" href="https://www.youtube.com/user/WSO2TechFlicks/playlists?view=50&sort=dd&shelf_id=8">Videos</a></li>
            </ul>
         </div>
         <div className="col-xl-1"></div>
      </div>
      
      <div className="row d-lg-none">
         <div className="col-12">
            <ul className="hot-links-list">
               <li><a className="hot-links-text" href="https://wso2is.slack.com/">Slack</a></li>
               <li><a className="hot-links-text" href="get-started/community/">Community</a></li>
               <li><a className="hot-links-text" href="https://wso2.com/blog/identity-and-access-management/">Blogs/Articles</a></li>
               <li><a className="hot-links-text" href="deploy/environment-compatibility/">Compatibility</a></li>
               <li><a className="hot-links-text" href="https://wso2.com/training/identity-server-fundamentals">Training</a></li>
               <li><a className="hot-links-text" href="https://store.wso2.com/store/assets/isconnector/list">Connectors</a></li>
               <li><a className="hot-links-text" href="https://www.youtube.com/user/WSO2TechFlicks/playlists?view=50&sort=dd&shelf_id=8">Videos</a></li>
            </ul>
         </div>
      </div>
   </div>
   <div className="container-fluid middle-container px-lg-5 py-5">
      <div className="row">
         <div className="col-xl-1"></div>
         <div className="col-xl-10">
            <h2 className="iam-secondary-heading">Integrate with Identity Server</h2>
            <p className="iam-secondary-text">
               Explore how you can integrate your applications with Identity Server to satisfy your IAM requirements. <br /> You can also use our sample applicaitons to try out common scenarios.
            </p>
         </div>
         <div className="col-xl-1"></div>
      </div>
      <div className="row">
         <div className="col-xl-1"></div>
         <div className="col-xl-10">
            <div className="row gy-3 gx-3">
               <div className="col-lg-4 col-sm-6 col-xs-12 position-relative">
                  <div className="card scenario-card">
                     <div className="card-body">
                        <h5 className="scenario-card-title-container">
                           <i className="material-icons-outlined scenario-card-icon pe-1">
                              <img src="assets/img/icons/landing-page/tick.svg" />
                           </i>
                           <div className="row scenario-card-title">
                              Enable Single Sign On
                           </div>
                        </h5>
                        <div className="ps-4">
                           <p className="scenario-card-text">
                              Allow users to securely log in to multiple applications by providing their credentials just once.
                           </p>
                           <div className="pb-4">
                              <a className="scenario-link-text" href="guides/login/sso-for-saml/">SAML</a><br />
                              <a className="scenario-link-text" href="guides/login/sso-for-oidc/">OAuth/OpenID Connect</a><br />
                              <a className="scenario-link-text" href="guides/login/configure-ws-federation-single-sign-on/">WS-Federation</a>
                           </div>
                           <div className="row position-absolute bottom-0 pb-3 scenario-dropdown">
                              <a className="try-it-out-text pt-2" rel="nofollow noopener">
                                 Try it out <i className="material-icons try-it-out-arrow">arrow_forward</i>
                              </a><br />
                              <div className="scenario-dropdown-content">
                                 <a href="quick-starts/single-sign-on/">Try out SSO using our sample applications</a>
                              </div>
                           </div>
                        </div>
                     </div>
                  </div>
               </div>
               <div className="col-lg-4 col-sm-6 col-xs-12 position-relative">
                  <div className="card scenario-card">
                     <div className="card-body">
                        <h5 className="scenario-card-title-container">
                           <i className="material-icons-outlined scenario-card-icon pe-1">
                              <img src="assets/img/icons/landing-page/user.svg" />
                           </i>
                           <div className="row scenario-card-title">
                              Add Federated Login
                           </div>
                        </h5>
                        <div className="ps-4">
                           <p className="scenario-card-text">
                              Enable users to log in using their social logins and integrate applications with enterprise identity providers.
                           </p>
                           <div className="pb-4">
                              <a className="scenario-link-text" href="guides/identity-federation/social-login/">Social logins</a><br />
                              <a className="scenario-link-text" href="guides/identity-federation/enterprise-identity-federation/">Protocol based login</a><br />
                           </div>
                           <div className="row position-absolute bottom-0 pb-3">
                              <a className="try-it-out-text pt-2" href="quick-starts/federated-authenticators" rel="nofollow noopener">
                                 Try it out <i className="material-icons try-it-out-arrow">arrow_forward</i>
                              </a><br />
                           </div>
                        </div>
                     </div>
                  </div>
               </div>
               <div className="col-lg-4 col-sm-6 col-xs-12 position-relative">
                  <div className="card scenario-card">
                     <div className="card-body">
                        <h5 className="scenario-card-title-container">
                           <i className="material-icons-outlined scenario-card-icon pe-1">
                              <img src="assets/img/icons/landing-page/admin.svg" />
                           </i>
                           <div className="row scenario-card-title">
                              Add Strong Authentication
                           </div>
                        </h5>
                        <div className="ps-4">
                           <p className="scenario-card-text">
                              Increase the number of authentication factors while still making sure your login process is user friendly.
                           </p>
                           <div className="pb-4">
                              <a className="scenario-link-text" href="guides/mfa/configure-authentication-journey/">Multi-factor authentication</a><br />
                              <a className="scenario-link-text" href="guides/adaptive-auth/configure-adaptive-auth/">Adaptive authentication</a><br />
                           </div>
                           <div className="row position-absolute bottom-0 pb-3 scenario-dropdown">
                              <a className="try-it-out-text pt-2">
                                 Try it out <i className="material-icons try-it-out-arrow">arrow_forward</i>
                              </a><br />
                              <div className="scenario-dropdown-content">
                                 
                                 <a href="quick-starts/adaptive-auth-overview/">Adaptive Authentication</a>
                              </div>
                           </div>
                        </div>
                     </div>
                  </div>
               </div>
               <div className="col-lg-4 col-sm-6 col-xs-12 position-relative">
                  <div className="card scenario-card">
                     <div className="card-body">
                        <h5 className="scenario-card-title-container">
                           <i className="material-icons-outlined scenario-card-icon pe-1">
                              <img src="assets/img/icons/landing-page/padlock.svg" />
                           </i>
                           <div className="row scenario-card-title">
                              Secure APIs
                           </div>
                        </h5>
                        <div className="ps-4">
                           <p className="scenario-card-text">
                              Enhance API security and ensure authorized access to your services and resources.
                           </p>
                           <div className="pb-4">
                              <a className="scenario-link-text" href="guides/access-delegation/oauth-grant-types/">OAuth grant types</a><br />
                              <a className="scenario-link-text" href="guides/access-delegation/uma">User managed access</a><br />
                           </div>
                           <div className="row position-absolute bottom-0 pb-3">
                              <a className="try-it-out-text pt-2" href="quick-starts/access-delegation/" rel="nofollow noopener">
                                 Try it out <i className="material-icons try-it-out-arrow">arrow_forward</i>
                              </a><br />
                           </div>
                        </div>
                     </div>
                  </div>
               </div>
               <div className="col-lg-4 col-sm-6 col-xs-12 position-relative">
                  <div className="card scenario-card">
                     <div className="card-body">
                        <h5 className="scenario-card-title-container">
                           <i className="material-icons-outlined scenario-card-icon pe-1">
                              <img src="assets/img/icons/landing-page/customer.svg" />
                           </i>
                           <div className="row scenario-card-title">
                              Manage Users
                           </div>
                        </h5>
                        <div className="ps-4">
                           <p className="scenario-card-text">
                              Deal with application users seamlessly throughout the identity lifecycle.
                           </p>
                           <div className="pb-4">
                              <a className="scenario-link-text" href="guides/identity-lifecycles/onboard-overview/">Onboard users</a><br />
                              <a className="scenario-link-text" href="guides/identity-lifecycles/manage-user-overview/">Manage users</a><br />
                              <a className="scenario-link-text" href="guides/identity-lifecycles/outbound-provisioning/">Outbound provision users</a><br />
                              <a className="scenario-link-text" href="guides/identity-lifecycles/inbound-provisioning/">Inbound provision users</a>
                           </div>
                        </div>
                     </div>
                  </div>
               </div>
               <div className="col-lg-4 col-sm-6 col-xs-12 position-relative">
                  <div className="card scenario-card">
                     <div className="card-body">
                        <h5 className="scenario-card-title-container">
                           <i className="material-icons-outlined scenario-card-icon pe-1">
                              <img src="assets/img/icons/landing-page/padlock.svg" />
                           </i>
                           <div className="row scenario-card-title">
                              Strengthen Privacy
                           </div>
                        </h5>
                        <div className="ps-4">
                           <p className="scenario-card-text">
                              Meet requirements of compliance frameworks and manage user consents.
                           </p>
                           <div className="pb-4">
                              <a className="scenario-link-text" href="references/concepts/compliance/compliance/">Regulatory compliance</a><br />
                              <a className="scenario-link-text" href="references/concepts/consent-management/">Consent management</a><br />
                           </div>
                        </div>
                     </div>
                  </div>
               </div>
            </div>
         </div>
         <div className="col-xl-1"></div>
      </div>
   </div>
   <div className="container-fluid px-lg-5 py-5">
      <div className="row">
         <div className="col-xl-1"></div>
         <div className="col-xl-10">
            <div className="row">
               <h2 className="iam-secondary-heading">Get to Know About Identity Server</h2>
               <p className="iam-secondary-text">
                  Learn about how the product is built, and how it can be efficiently deployed and upgraded.
               </p>
            </div>
            <div className="row gy-4 px-sm-1">
               <div className="col-xl-3 col-sm-6 col-xs-12 position-relative">
                  <div className="row">
                     <div className="card icon-card">
                        <i className="material-icons-outlined icon-font">
                           <img className="bottom-icon" src="assets/img/icons/landing-page/announce.svg" />
                        </i>
                     </div>
                  </div>
                  <div className="row pb-2">
                     <h3 className="more-info-heading-text">What's new in WSO2 IS 5.11.0</h3>
                     <p className="more-info-text">
                        Get to know the new features and the enhancements in this release.
                     </p>
                  </div>
                  <div className="row position-absolute bottom-0">
                     <a className="learn-more-text fw-bold" href="get-started/about-this-release/">
                        Learn More <i className="material-icons learn-more-arrow">arrow_right_alt</i>
                     </a>
                  </div>
               </div>
               <div className="col-xl-3 col-sm-6 col-xs-12 position-relative">
                  <div className="row">
                     <div className="card icon-card">
                        <i className="material-icons-outlined icon-font">
                           <img className="bottom-icon" src="assets/img/icons/landing-page/setting.svg" />
                        </i>
                     </div>
                  </div>
                  <div className="row pb-2">
                     <h3 className="more-info-heading-text">WSO2 IS Architecture</h3>
                     <p className="more-info-text">
                        Learn about the componentized architecture of WSO2 IS and the process flow.
                     </p>
                  </div>
                  <div className="row position-absolute bottom-0">
                     <a className="learn-more-text fw-bold" href="get-started/architecture/">
                        Learn More <i className="material-icons learn-more-arrow">arrow_right_alt</i>
                     </a>
                  </div>
               </div>
               <div className="col-xl-3 col-sm-6 col-xs-12 position-relative">
                  <div className="row">
                     <div className="card icon-card">
                        <i className="material-icons-outlined icon-font">
                           <img className="bottom-icon" src="assets/img/icons/landing-page/outline.svg" />
                        </i>
                     </div>
                  </div>
                  <div className="row pb-2">
                     <h3 className="more-info-heading-text">Deployment Best Practices</h3>
                     <p className="more-info-text">
                        Apply recommended deployment practices to enhance security and performance.
                     </p>
                  </div>
                  <div className="row position-absolute bottom-0 pt-4">
                     <a className="learn-more-text fw-bold" href="deploy/deployment-checklist/">
                        Learn More <i className="material-icons learn-more-arrow">arrow_right_alt</i>
                     </a>
                  </div>
               </div>
               <div className="col-xl-3 col-sm-6 col-xs-12 position-relative">
                  <div className="row">
                     <div className="card icon-card">
                        <i className="material-icons-outlined icon-font">
                           <img className="bottom-icon" src="assets/img/icons/landing-page/swap.svg" />
                        </i>
                     </div>
                  </div>
                  <div className="row pb-2">
                     <h3 className="more-info-heading-text">Migrate to WSO2 IS 5.11.0</h3>
                     <p className="more-info-text">
                        Upgrade to the latest version to receive all new updates of the product.
                     </p>
                  </div>
                  <div className="row position-absolute bottom-0 pt-4">
                     <a className="learn-more-text fw-bold" href="deploy/migrate/migrate-to-5110/">
                        Learn More <i className="material-icons learn-more-arrow">arrow_right_alt</i>
                     </a>
                  </div>
               </div>
            </div>
         </div>
         <div className="col-xl-1"></div>
      </div>
   </div>
</div>
