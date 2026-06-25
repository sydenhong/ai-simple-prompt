Please update the QR payment modal UI to KHQR style.

Goal:
Redesign the payment QR modal to look like an official KHQR payment card, while keeping all existing payment logic unchanged.

Requirements:

1. KHQR Header

* Add a red KHQR-style header at the top of the payment card.
* Header background color: `#E1251B`.
* Header should have rounded top-left and top-right corners.
* Use this KHQR white logo:
  `https://ypufoeychtydvaughsrg.supabase.co/storage/v1/object/public/bantub/KHQR_logo_white_v2.png`
* Logo must be white, clear, centered, and not transparent.
* Do not apply opacity, filter, shadow, blend mode, or red color to the logo.
* Logo size should be clean, around `h-8` or `h-9`.

2. Right-side KHQR Notch

* The right-side notch must match the KHQR reference.
* Do not use `clipPath` on the whole red header.
* Do not make the whole header look like an arrow.
* Keep the red header as a normal rectangle.
* Add a separate red diagonal triangle/notch at the bottom-right of the header.
* The red notch should extend down into the white card body.
* The top-right corner must remain rounded.
* The notch must use the same red color as the header: `#E1251B`.

Suggested JSX structure:

```tsx
<div className="relative h-16 sm:h-[72px] bg-[#E1251B] flex items-center justify-center text-white overflow-visible">
  <img
    src="https://ypufoeychtydvaughsrg.supabase.co/storage/v1/object/public/bantub/KHQR_logo_white_v2.png"
    alt="KHQR"
    className="h-8 sm:h-9 w-auto object-contain"
  />

  <div
    className="absolute right-0 bottom-[-46px] w-[54px] h-[46px] bg-[#E1251B]"
    style={{
      clipPath: 'polygon(0 0, 100% 100%, 100% 0)',
    }}
  />
</div>
```

3. Card Body

* Show merchant/business name below the header.
* Show the latest dynamic payment amount below the merchant name.
* Currency must be Riel only.
* Format example: `2,500៛`
* Do not show Dollar currency anywhere.
* Amount must come from the latest user-selected total, not a hardcoded value.

4. QR Section

* Show QR code large, centered, and easy to scan.
* Keep enough white padding around QR.
* QR value must come from the existing payment API response.
* Do not change QR generation logic.

5. Timer

* Countdown starts from 10 minutes.
* Format: `MM:SS`, example `09:44`.
* Timer turns red during the last 60 seconds.
* When timer reaches `00:00`, stop checking payment and show QR expired state.
* Allow user to generate a new QR again.

6. Payment Checking

* Keep existing payment checking logic.
* Check payment only while:

  * modal is open
  * QR is not expired
  * payment is not completed
* Stop checking when:

  * payment succeeds
  * user cancels/closes modal
  * QR expires
  * component unmounts
* Prevent duplicate intervals.

7. Actions

* Remove top-right close button.
* Add bottom action buttons:

  * Share
  * Download
  * Copy
  * Cancel
* Cancel button should be red or light-red style.

8. Cancel Confirmation

* When user clicks Cancel, do not close immediately.
* Show confirmation popup.
* Buttons:

  * Continue Payment
  * Close
* Continue Payment closes only the confirmation popup.
* Close closes the QR modal and stops payment checking.

Important:

* Update UI only.
* Do not break payment API logic.
* Do not change amount calculation logic.
* Do not change currency logic.
* Currency is Riel only: `៛`
* Make sure TypeScript/React has no errors.
* Provide full updated component code.
