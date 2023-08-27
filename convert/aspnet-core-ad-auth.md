Title: Authenticate Users By AD Group In An ASP.NET Core App
Date: 2021-12-01 14:07:00
Modified: 2021-12-02 10:49:00
Category: Python
Tags: pelican, publishing
Slug: ad-group-authentication-asp-net-core-app
Summary: Authenticate Users By AD Group In An ASP.NET Core App
Status: published


To restrict access to an ASP.NET Core application via Active Directory group membership:

- Set authentication in IIS for the given site so that only "Windows Authentication" is enabled.
- Modify your Startup.cs to add authentication and an authorization policy requiring a role (i.e. AD group membership)
- Add the [Authorize] attribute to any controller to be locked down.

ex: Startup.cs

    using System;
    using System.Collections.Generic;
    using System.Linq;
    using System.Threading.Tasks;
    using Microsoft.AspNetCore.Authorization;
    using Microsoft.AspNetCore.Builder;
    using Microsoft.AspNetCore.Hosting;
    using Microsoft.AspNetCore.Mvc.Authorization;
    using Microsoft.AspNetCore.Server.IISIntegration;
    using Microsoft.Extensions.Configuration;
    using Microsoft.Extensions.DependencyInjection;
    using Microsoft.Extensions.Hosting;

    namespace Boilerplate
    {
        public class Startup
        {
            public Startup(IConfiguration configuration)
            {
                Configuration = configuration;
            }

            public IConfiguration Configuration { get; }

            // This method gets called by the runtime. Use this method to add services to the container.
            public void ConfigureServices(IServiceCollection services)
            {
                services.AddAuthentication(IISDefaults.AuthenticationScheme);
                services.AddAuthorization(options =>
                {
                    options.AddPolicy("ADRoleOnly", policy => policy.RequireRole("MYDOMAIN\\SOMEADGROUP"));
                });
                ...
                services.AddMvc(config =>
                {
                    var policy = new AuthorizationPolicyBuilder()
                        .RequireAuthenticatedUser()
                        .Build();

                    config.Filters.Add(new AuthorizeFilter(policy));
                });
            }

            // This method gets called by the runtime. Use this method to configure the HTTP request pipeline.
            public void Configure(IApplicationBuilder app, IWebHostEnvironment env)
            {
                if (env.IsDevelopment())
                {
                    app.UseDeveloperExceptionPage();
                }
                else
                {
                    app.UseExceptionHandler("/Home/Error");
                }
                app.UseStaticFiles();

                app.UseRouting();

                app.UseAuthorization();

                app.UseStatusCodePages(async context => {
                    if (context.HttpContext.Response.StatusCode == 403)
                    {
                        // your redirect
                        context.HttpContext.Response.Redirect("/Home/Error");
                    }
                });

                app.UseEndpoints(endpoints =>
                {
                    endpoints.MapControllerRoute(
                        name: "default",
                        pattern: "{controller=Home}/{action=Index}/{id?}");
                });
            }
        }
    }

** Apply to given controllers... **

    namespace Boilerplate.Controllers
    {
        [Authorize(Policy = "ADRoleOnly")]
        public class HomeController : Controller
    ....
