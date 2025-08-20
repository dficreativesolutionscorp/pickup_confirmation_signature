# DFI Rentals Pickup Confirmation System

## Overview

This is a web-based tablet application designed for DFI Rentals to digitally confirm equipment pickups. The application integrates with the Booqable rental management API to fetch order details, capture customer signatures, and generate pickup confirmation documents.

## Key Features

### 1. Order Retrieval
- Simple order lookup by order number
- Fetches complete order details from Booqable API
- Displays customer information, rental dates, and pricing

### 2. Equipment Checklist
- Interactive checkbox list for all rental items
- Supports bundle items with parent-child relationships
- Displays product images, quantities, and extra information
- Prevents signature until all items are checked

### 3. Terms & Conditions
- Multiple acknowledgment checkboxes for legal requirements
- Links to full rental agreement
- Ensures customer understands their responsibilities

### 4. Digital Signature Capture
- HTML5 canvas-based signature pad
- Touch and mouse support for tablets and desktop
- Name capture for identification
- Signature required before confirmation

### 5. Email Options
- Choice between sending to customer's email on file
- Option to specify alternative email address
- Email validation for custom addresses

### 6. Document Generation
- Automatically creates contract document via Booqable API
- Attaches digital signature to the document
- Adds signer name to document footer
- Sends email confirmation with attached contract

### 7. Security Features
- Lock screen after successful pickup
- Slide-to-unlock mechanism
- 4-digit passcode (1080) required to reset
- Prevents accidental access to new orders

## Technical Details

### API Integration
- **Booqable API v4**: Primary API for order management
- **Booqable API v1**: Used for legacy order lookup
- **Authentication**: Bearer token authentication
- **Endpoints Used**:
  - `/api/1/orders/{number}` - Fetch order details
  - `/api/4/documents/` - Create contract documents
  - `/api/4/signatures/` - Attach signatures
  - `/api/4/emails/` - Send confirmation emails

### User Flow

1. **Order Entry**
   - Staff enters order number
   - System fetches order from Booqable

2. **Order Review**
   - Customer views order details including:
     - Order number and dates
     - Customer information
     - Rental period
     - All equipment items with images
     - Pricing breakdown (subtotal, discounts, tax, total)
     - Estimated replacement value

3. **Item Verification**
   - Customer checks each item as received
   - System prevents proceeding until all items checked

4. **Terms Acceptance**
   - Customer acknowledges all 5 required terms
   - Links to full rental agreement provided

5. **Email Selection**
   - Customer chooses email destination
   - Can use email on file or specify different address

6. **Signature Capture**
   - Customer enters their name
   - Signs on touchscreen
   - Can clear and retry if needed

7. **Confirmation**
   - System generates contract document
   - Attaches signature
   - Sends email confirmation
   - Locks interface

8. **Reset**
   - Staff uses slide-to-unlock
   - Enters passcode (1080)
   - System ready for next customer

### Design Features

- **Responsive Design**: Works on tablets and desktop browsers
- **Touch Optimized**: Large buttons and touch targets
- **Visual Hierarchy**: Clear sections and information grouping
- **DFI Branding**: Uses company colors and logo
- **Real-time Clock**: Shows current date/time in header

### Data Handling

- **Order Data Structure**:
  - Customer details (name, email)
  - Line items (products, bundles, sections)
  - Pricing (subtotal, discounts, tax, total)
  - Rental period (start/end dates)
  - Coupon information

- **Line Item Types**:
  - Regular items: Individual rental products
  - Bundle items: Group of related products
  - Section items: Visual separators in the order
  - Child items: Products within a bundle

### Security Considerations

- API key is embedded (should be server-side in production)
- No persistent storage - all data session-based
- Lock screen prevents unauthorized access
- Passcode protection for staff reset

## Configuration

Key configuration values in the code:

```javascript
const API_KEY = '47c4f6c39f9666034face985d225a522b60c3ae8fd923fae6af9bca907e2caf5';
const API_BASE = 'https://dfi-rentals.booqable.com/api/4';
const UNLOCK_PASSCODE = '1080';
const EMAIL_TEMPLATE_ID = '977ff0cc-0fbd-432d-a1b3-effe01d94fab';
```

## Browser Requirements

- Modern browser with HTML5 canvas support
- Touch events support for tablet use
- JavaScript enabled
- Internet connection for API access

## Known Limitations

1. API key exposed in client-side code
2. No offline capability
3. No signature image storage backup
4. Email sending errors don't block confirmation
5. No multi-language support

## Future Enhancements

Potential improvements could include:
- Server-side API proxy for security
- Offline mode with sync capability
- Multiple signature capture (customer + staff)
- Photo capture of equipment condition
- Integration with payment processing
- Multi-location support
- Analytics and reporting
