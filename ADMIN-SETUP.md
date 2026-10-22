# Club Bolts admin dashboard

Admin page: https://mjpdeflew-ship-it.github.io/3432/admin.html

## Product management

The dashboard already includes an **Add product** action, catalogue search and filters, product editing, availability toggles, deletion, order management, and store settings. Product changes are saved to Supabase and then appear on the storefront according to stock status.

## Import 300 common products

After signing in, open **Products** and choose **Import 300 common products**. This adds common metric hex/socket/carriage/flange/anchor bolts, pan/countersunk/machine/self-tapping/wood screws, several nut styles, and flat/spring/fender/lock/sealing washers in sizes M4, M5, M6, M8, M10, and M12. Where the material column is configured, 24 entries are stainless steel; otherwise the importer uses 300 steel entries. Existing matching products are skipped to avoid duplicates.

The import prices are **starter estimates in EGP, not verified supplier quotations**. The importer asks for confirmation before making the entries visible as in-stock products. Confirm your own buying costs and selling prices, and verify actual stock, before accepting customer orders.

## One-time secure setup

1. In the Supabase dashboard for this project, open **SQL Editor**.
2. Open the repository file [admin-policies.sql](https://github.com/mjpdeflew-ship-it/3432/blob/main/admin-policies.sql), copy its full contents into the SQL Editor, and run it once. Review the SQL before running it because it configures database access policies.
3. In Supabase, open **Authentication → Users** and create the owner account with an email and password.
4. In the SQL Editor, replace `YOUR_ADMIN_EMAIL@example.com` in the commented one-time admin statement at the bottom of `admin-policies.sql`, uncomment that statement, and run it. It marks only that Auth user's trusted `app_metadata.role` as `admin`.
5. Sign in at the admin URL above. If you were already signed in, sign out and back in so the session token includes the updated role.

Do not add a Supabase service-role key, database password, or other secret to `config.js` or any browser file. The public publishable/anon key is intended for browser use; database Row Level Security policies must remain enabled.

## Adding a product

1. Sign in to the admin page.
2. Select **Products → Add product** (or use **Add a product** from Overview).
3. Choose a category, enter the product type, metric size, optional length, material, price in EGP, and stock availability.
4. Save the product. If it is marked out of stock, it remains in the admin catalogue but is hidden from customers by the storefront's in-stock query.

If a save fails with a permission error, verify that the owner account was assigned the admin role and sign in again. Check the Supabase API/database logs for schema or RLS errors; do not disable RLS to make the dashboard work.
